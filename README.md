# Gemini generator for PHP
	$senderAccountPrefix = null;
	$senderAccountNumber = '1234567890';
	$senderBankCode = '5500'; // 4 numbers

	$gemini = new Gemini();
	$gemini->setSender($senderBankCode, $senderAccountNumber, $senderAccountPrefix);
	foreach ($this->getPaymentItems() as $i) {
		$fullAccountNumber = $i->accountPrefix . $i->accountNumber . '/' . $i->bankCode;
		$item = (new Item($fullAccountNumber, $i->amount, $i->varSym))
			->setConstSym($i->constSym ?? '')
			->setSpecSym($i->specSym ?? '')
			->setMessage($i->message ?? '')
			;
		$gemini->addItem($item);
	}
	$res = $gemini->generate();


	echo '<pre>' . $res . '</pre>';
