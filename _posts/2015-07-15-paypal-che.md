---
title: PayPal Checkout to Your 3rd-party Shopping Cart
author: PipisCrew
date: 2015-07-15
categories: []
toc: true
---

alternative [http://fastspring.com/developer-support](http://fastspring.com/developer-support)  -or-  [http://github.com/FastSpring/](http://github.com/FastSpring/)

[http://www.paypal.com/cgi-bin/webscr?cmd=p/pdn/howto_checkout-outside](http://www.paypal.com/cgi-bin/webscr?cmd=p/pdn/howto_checkout-outside)

at html for @email.com use urname%40gmail.com

sample by philip
```js
//test

    $(document).ready(function($) {

        $('#paypal_time').on('click', function(e) {
//            e.preventDefault();
            empty_cart();

         	//add paypal account dynamic, so no spam :)
            $('<input>').attr({type:'hidden', class:'cart_destination', name:'business', value:"x@x.com"}).prependTo('#shopping_cart');

            fill_cart();
        });

        $('#paypal_reset').on('click', function(e) {    
            empty_cart();
        });
    });

    function empty_cart(){
        $("#shopping_cart .cart_item").remove();
        $("#shopping_cart .cart_destination").remove();
    }

    function fill_cart() {
        var cart_item_list = 4;
         product_counter=0;

//warning the item #product_counter# should be linear (1/2/3/4), otherwise only the first will be accepted
        for (i = 1; i < cart_item_list;="" i++){="" if="" (i="=1){" var="" chosen_item_name="Number One" ;="" var="" chosen_item_quantity="1;" var="" chosen_item_cost="35.00;" var="" chosen_item_shipping_single="1.35;" var="" chosen_item_shipping_double="0.35;" var="" chosen_curr="USD" ;="" var="" sku_no="1sd3423f" ;="" }="" if="" (i="=2){" var="" chosen_item_name="Number Two" ;="" var="" chosen_item_quantity="3;" var="" chosen_item_cost="32.00;" var="" chosen_item_shipping_single="1.50;" var="" chosen_item_shipping_double="0.50;" var="" chosen_curr="USD" ;="" var="" sku_no="9dasf" ;="" }="" if="" (i="=3){" var="" chosen_item_name="Number Three" ;="" var="" chosen_item_quantity="2;" var="" chosen_item_cost="40.00;" var="" chosen_item_shipping_single="4.00;" var="" chosen_item_shipping_double="0.80;" var="" chosen_curr="USD" ;="" var="" sku_no="93284" ;="" }="" create_form_element(sku_no,chosen_item_name,="" chosen_item_cost,="" chosen_item_quantity);="" }="" }="" var="" product_counter;="" function="" create_form_element(sku,product_title,cost,quantity)="" {="" product_counter+="1;" var="" shipping_num="2;" var="" chosen_curr="USD" ;="" var="" chosen_item_shipping_single="4.00;" var="" chosen_item_shipping_double="0.80;"><input>').attr({type:'hidden', class:'cart_item', name:'upload', value:product_counter}).appendTo('#shopping_cart');
        $('<input>').attr({type:'hidden', class:'cart_item', name:('item_name_' + product_counter), value:product_title}).appendTo('#shopping_cart');
        $('<input>').attr({type:'hidden', class:'cart_item', name:('quantity_' + product_counter), value:quantity}).appendTo('#shopping_cart');
        $('<input>').attr({type:'hidden', class:'cart_item', name:('amount_' + product_counter), value:cost}).appendTo('#shopping_cart');
        $('<input>').attr({type:'hidden', class:'cart_item', name:('item_number_' + product_counter), value:sku}).appendTo('#shopping_cart');
        $('<input>').attr({type:'hidden', class:'cart_item', name:('shipping_' + product_counter), value:chosen_item_shipping_single}).appendTo('#shopping_cart');
//        $('<input>').attr({type:'hidden', class:'cart_item', name:('shipping'+shipping_num+'_' + product_counter), value:chosen_item_shipping_double}).appendTo('#shopping_cart');
        $('<input>').attr({type:'hidden', class:'cart_item', name:('currency_code_' + product_counter), value:chosen_curr}).appendTo('#shopping_cart');

    }

# 2o15 example

        <form action="https://www.paypal.com/cgi-bin/webscr" method="post" id="shopping_cart">
            <input type="hidden" name="charset" value="utf-8"> 

            <input type="hidden" name="cmd" value="_cart">

            <input type="image" id="paypal_time" src="http://www.paypal.com/en_US/i/btn/x-click-but01.gif" name="submit" alt="Make payments with PayPal - it's fast, free and secure!">
        </form>
        <button id="paypal_reset">Reset</button>

```

## sample of generated form 

```js
<form action="https://www.paypal.com/cgi-bin/webscr" method="post" id="shopping_cart">
	<input type="hidden" name="charset" value="utf-8"> 
	<input type="hidden" class="cart_destination" name="business" value="x@x.com">

	<input type="hidden" name="cmd" value="_cart">

	<input type="image" id="paypal_time" src="http://www.paypal.com/en_US/i/btn/x-click-but01.gif" name="submit" alt="Make payments with PayPal - it's fast, free and secure!">

	<input type="hidden" class="cart_item" name="upload" value="1">
	<input type="hidden" class="cart_item" name="item_name_1" value="Number One">
	<input type="hidden" class="cart_item" name="quantity_1" value="1">
	<input type="hidden" class="cart_item" name="amount_1" value="35">
	<input type="hidden" class="cart_item" name="item_number_1" value="1sd3423f">
	<input type="hidden" class="cart_item" name="shipping_1" value="4">
	<input type="hidden" class="cart_item" name="currency_code_1" value="USD">

	<input type="hidden" class="cart_item" name="upload" value="2">
	<input type="hidden" class="cart_item" name="item_name_2" value="Number Two">
	<input type="hidden" class="cart_item" name="quantity_2" value="3">
	<input type="hidden" class="cart_item" name="amount_2" value="32">
	<input type="hidden" class="cart_item" name="item_number_2" value="9dasf">
	<input type="hidden" class="cart_item" name="shipping_2" value="4">
	<input type="hidden" class="cart_item" name="currency_code_2" value="USD">

	<input type="hidden" class="cart_item" name="upload" value="3">
	<input type="hidden" class="cart_item" name="item_name_3" value="Number Three">
	<input type="hidden" class="cart_item" name="quantity_3" value="2">
	<input type="hidden" class="cart_item" name="amount_3" value="40">
	<input type="hidden" class="cart_item" name="item_number_3" value="93284">
	<input type="hidden" class="cart_item" name="shipping_3" value="4">
	<input type="hidden" class="cart_item" name="currency_code_3" value="USD">
</form>
```

## Using Paypal Sandbox

reference 
[http://www.paypal.com/cgi-bin/webscr?cmd=p/sell/ipn-test-outside](http://www.paypal.com/cgi-bin/webscr?cmd=p/sell/ipn-test-outside)

1-on our form the action should converted to https://www.sandbox.paypal.com/cgi-bin/webscr as also, the seller mail should be used the one generated on step 2
2-goto [http://developer.paypal.com](http://developer.paypal.com) login with your business account, create virtual buyer & seller accounts, use it to make the tests!

## Responses

source - [http://stackoverflow.com/a/16672181](http://stackoverflow.com/a/16672181)
<strong style="color:red">notify-url** and <strong style="color:red">return url** both are different . your <strong style="color:red">return url** direct your customer after the successful payment with some return information. by the way <strong style="color:red">notify url** is to get the complete transaction details of your customers purchase and which can't be accessed by your customer and this is for your database or storage purpose.

* * *

using sandbox, the <strong style="color:red">return url** doesnt return anything.

at <strong style="color:red">notify-url** using 
```js
//source http://developer.paypal.com/docs/classic/ipn/ht_ipn/

$raw_post_data = file_get_contents('php://input');
$raw_post_array = explode('&', $raw_post_data);
$myPost = array();
foreach ($raw_post_array as $keyval) {
  $keyval = explode ('=', $keyval);
  if (count($keyval) == 2)
     $myPost[$keyval[0]] = urldecode($keyval[1]);
}
.
.
```

returns :

```js
mc_gross=18.00
protection_eligibility=Eligible
address_status=confirmed
item_number1=21101
tax=0.00
item_number2=70
payer_id=JHfNL45Q2
item_number3=67
address_street=1+Main+St
payment_date=05%3A21%3A02+Jul+08%2C+2015+PDT
payment_status=Completed
charset=windows-1252
address_zip=95131
mc_shipping=0.00
mc_handling=0.00
first_name=test
mc_fee=0.82
address_country_code=US
address_name=test+buyer¬ify_version=3.8
custom=
payer_status=verified
business=x-facilitator%40x.com
address_country=United+States
num_cart_items=3
mc_handling1=0.00
mc_handling2=0.00
mc_handling3=0.00
address_city=San+Jose
verify_sign=Afcf.0wMpKgV9A4.VEDWAQ0u5Ju5VbNdZNbVnIxb0LvFqU.Y
payer_email=x-buyer%40x.com
mc_shipping1=0.00
mc_shipping2=0.00
mc_shipping3=0.00
tax1=0.00
tax2=0.00
tax3=0.00
memo=my+test
txn_id=2Vf7662L
payment_type=instant
last_name=buyer
address_state=CA
item_name1=iThmb+Converter+v1+%28medium2%29
receiver_email=x-facilitator%40x.com
item_name2=wide
payment_fee=0.82
item_name3=my+new+title
quantity1=2
quantity2=1
receiver_id=UFfSTUA
quantity3=1
txn_type=cart
mc_gross_1=6.00
mc_currency=USD
mc_gross_2=8.00
mc_gross_3=4.00
residence_country=US
test_ipn=1
transaction_subject=
payment_gross=18.00
ipn_track_id=2fff141bb 
```

line 4/6/8 = item_number (aka SKU) posted by our form
line 47/48/50 = items quantity posted by our form
line 37 = comment added on paypal purchase by user
line 11/38/51 = transaction identity + transaction status
line 20 = custom, pass any string @ form, will be returned on IPN^

//[https://developer.paypal.com/docs/classic/ipn/ht_ipn/](https://developer.paypal.com/docs/classic/ipn/ht_ipn/)
the flow is to 
1-take the response 
2-send it back to paypal
3-reply VERIFIED or INVALID

### ^tested only with sandbox no working

IPN used only @ form post <strong style="color:red">notify_url**.. Totally lost... 
![](https://www.pipiscrew.com/wp-content/uploads/2015/06/snap160.png "snap160")

then search&found @ http://paypal.com 
![](https://www.pipiscrew.com/wp-content/uploads/2015/06/snap155.png "snap155")
which IPN URL setted, but I didnt got any response (maybe because my form for the mom post to https://www.sandbox.paypal.com/cgi-bin/webscr), who knows.. 

will be updated, when test it, via real card..

--update
today I made a real transaction w/ real paypal account my form looks like 
```js
			        <form action="https://www.paypal.com/cgi-bin/webscr" method="post" id="shopping_cart">

			            <input type="hidden" name="cmd" value="_cart">
						<input type="hidden" name="charset" value="utf-8">
						<input type="hidden" class="cart_destination" name="business" value="<?= $paypal_address; ?>">
						<input type="hidden" name="notify_url" value="<?= $cms_url; ?>pay_info.php">
						<input type="hidden" name="return" value="<?= $cms_url; ?>pay_success_return.php">
						<input type="hidden" name="cancel_return" value="<?= $cms_url; ?>pay_cancel.php">
						<input type="hidden" name="custom" value="<?= " pipiscrew";="">">

<?= $paypal_form_elements;?=""?>

						<input type="image" id="paypal_time" class="img-responsive" src="assets/payment_paypal.png" name="submit" alt="Make payments with PayPal - it's fast, free and secure!">

			        </form>
```

finally!! 

the paypal.com>settings> profile settings>my selling tools>instant payment notifications was/is **OFF** 

I got the feedback @ <strong style="color:red;">notify_url** setted on **form**^^

[![](https://www.pipiscrew.com/wp-content/uploads/2015/06/snap171.jpg "snap171")](https://www.pipiscrew.com/wp-content/uploads/2015/06/snap171.jpg)

* * *

## the simple solution

source - [http://stackoverflow.com/a/9241669](http://stackoverflow.com/a/9241669)
The <strong style="color:red">txn_id** is unique for each transaction, not each IPN message. What this means is; one transaction can have multiple IPN messages. eCheck, for example, where it will go in a 'Pending' state by default, and 'Complete' once the eCheck has cleared.
But you may also see reversals, canceled reversals, cases opened and refunds against the same txn_id.

```js
//Pseudo code:

If not empty txn_id and txn_type = web_accept and payment_status = Completed  
    // New payment received; completed. May have been a transaction which was pending earlier.
    Update database set payment_status = Completed and txn_id = $_POST['txn_id']  

If not empty txn_id and txn_type = web_accept and payment_status = Pending  
    // New payment received; completed  
    Update database set payment_status = Pending and payment_reason = $_POST['pending_reason'] and txn_id = $_POST['txn_id']
```

* * *

## Instant Payment Notification (IPN)

[http://developer.paypal.com/docs/classic/products/instant-payment-notification/](http://developer.paypal.com/docs/classic/products/instant-payment-notification/)
[http://developer.paypal.com/docs/classic/ipn/ht_ipn/](http://developer.paypal.com/docs/classic/ipn/ht_ipn/)

* * *

> PayPal Return URL not called, except when payer_status = verified?

 if the purchaser uses Guest Checkout, e.g. pays with a credit card, the RETURN URL is NOT triggered.
[http://stackoverflow.com/q/17640861](http://stackoverflow.com/q/17640861)

* * *

> How to Create One-Time Payments Using Express Checkout

[https://developer.paypal.com/docs/classic/express-checkout/integration-guide/ECGettingStarted/](https://developer.paypal.com/docs/classic/express-checkout/integration-guide/ECGettingStarted/)

[http://developer.paypal.com/docs/classic/express-checkout/ht_ec-singleItemPayment-curl-etc/](http://developer.paypal.com/docs/classic/express-checkout/ht_ec-singleItemPayment-curl-etc/)

* * *

> Redirect user to Paypal via PHP

[http://stackoverflow.com/a/14843758](http://stackoverflow.com/a/14843758)</strong></strong></strong></strong></strong></strong></strong></strong></strong>

origin - http://www.pipiscrew.com/?p=3219 paypal-checkout-to-your-3rd-party-shopping-cart