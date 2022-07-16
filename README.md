# ZarinPal Advanced Class + Laravel
ZarinPal Advanced Class AND PHP Sample Code + Laravel Totorial


Document : https://miladworkshop.ir/blog/26-zarinpal-advanced-class.html XD
# Laravel Usage
* create folder to root App project -> App/Libs
* add Zarinpal.php Here
* use namespase and work it! XD

# Sample Reuest PHP Code :

```php
<?php
require_once("zarinpal_function.php");
//or in laravel
use App/Libs/Zarinpal;


$MerchantID 	          = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx";
$Amount 		  = 100;
$ZarinGate 		  = false;
$SandBox 		  = false;

$zp 	= new Zarinpal();
$result = $zp->verify($MerchantID, $Amount, $SandBox, $ZarinGate);

if (isset($result["Status"]) && $result["Status"] == 100)
{
	// Success
	echo "تراکنش با موفقیت انجام شد";
	echo "<br />مبلغ : ". $result["Amount"];
	echo "<br />کد پیگیری : ". $result["RefID"];
	echo "<br />Authority : ". $result["Authority"];
} else {
	// error
	echo "پرداخت ناموفق";
	echo "<br />کد خطا : ". $result["Status"];
	echo "<br />تفسیر و علت خطا : ". $result["Message"];
}
?>
```

# Sample Verify PHP Code :

```php
<?php
require_once("zarinpal_function.php");
//or in laravel
use App/Libs/Zarinpal;

$MerchantID 	     = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx";
$Amount           = 100;
$Description 	  = "تراکنش زرین پال";
$Email 			= "";
$Mobile 		= "";
$CallbackURL 	    = "http://example.com/verify.php";
$ZarinGate 		  = false;
$SandBox 		  = false;

$zp 	= new Zarinpal();
$result = $zp->request($MerchantID, $Amount, $Description, $Email, $Mobile, $CallbackURL, $SandBox, $ZarinGate);

if (isset($result["Status"]) && $result["Status"] == 100)
{
	// Success and redirect to pay
	$zp->redirect($result["StartPay"]);
} else {
	// error
	echo "خطا در ایجاد تراکنش";
	echo "<br />کد خطا : ". $result["Status"];
	echo "<br />تفسیر و علت خطا : ". $result["Message"];
}
?>
```
