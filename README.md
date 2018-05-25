# PaymentMollie
[Mollie](https://www.mollie.com/be/) payment method for [ProcessWire](https://processwire.com/)

## Requirements
Requires [PaymentModule -module](http://modules.processwire.com/modules/payment-module/)

## Mollie API

(Info form https://github.com/mollie/mollie-api-php)

To use the Mollie API client, the following things are required:

+ Get yourself a free [Mollie account](https://www.mollie.com/signup). No sign up costs.
+ Now you're ready to use the Mollie API client in test mode.
+ Follow [a few steps](https://www.mollie.com/dashboard/?modal=onboarding) to enable payment methods in live mode, and let us handle the rest.
+ PHP >= 5.6
+ Up-to-date OpenSSL (or other SSL/TLS toolkit)

### Composer Installation ###

By far the easiest way to install the Mollie API client is to require it with [Composer](http://getcomposer.org/doc/00-intro.md).

    $ composer require mollie/mollie-api-php:^2.0

    {
        "require": {
            "mollie/mollie-api-php": "^2.0"
        }
    }

The version of the API client corresponds to the version of the API it implements. Check the [notes on migration](https://docs.mollie.com/migrating-v1-to-v2) to see what changes you need to make if you want to start using a newer API version.

### Manual Installation ###
If you're not familiar with using composer we've added a ZIP file to the releases containing the API client and all the packages normally installed by composer.
Download the ``mollie-api-php.zip`` from the [releases page](https://github.com/mollie/mollie-api-php/releases).

Include the ``vendor/autoload.php`` as shown in [Initialize example](https://github.com/mollie/mollie-api-php/blob/master/examples/initialize.php).

## Example (with [Padloper](https://www.padloper.pw/))

```PHP

$checkout = modules()->get("PadOnePageCheckout");
$checkout->setPaymentModule("PaymentMollie");
$payment = modules()->get("PaymentMollie");

$urlSegment = input()->urlSegment1;

if (input()->urlSegment1 == "payment") {
    $payment->processPayment();
    exit;
}

if (!input()->urlSegment1 && input()->get('id')) {

    // Check the order
    $order = pages()->get(input()->get('id'));

    // Check if the order has been paid
    if($order->pad_paid){
        session()->redirect(page()->url."success");
        exit;

    }else{
        session()->redirect(page()->url."confirmation");
        exit;
    }
}

```

## License
MIT License
