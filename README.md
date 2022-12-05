
# Cordova ClickPay Plugin
![Version](https://img.shields.io/badge/Cordova%20ClickPay%20Plugin-v1.3.1-green)
[![npm](https://img.shields.io/npm/l/cordova-plugin-ClickPay.svg)](https://www.npmjs.com/package/cordova-plugin-ClickPay/)
[![npm](https://img.shields.io/npm/dm/cordova-plugin-ClickPay.svg)](https://www.npmjs.com/package/cordova-plugin-ClickPay)

Cordova ClickPay Plugin is a wrapper for the native ClickPay Android and iOS SDKs, It helps you integrate with ClickPay payment gateway.

Plugin Support:

* [x] iOS
* [x] Android

# Installation

```
$ cordova plugin add '@clickpay.sa/cordova.plugin.clickpay'
```

### Android - Prerequisites
Open `gradle.properties` and set the flags useAndroidX and enableJetifier with true.

```
android.useAndroidX=true
android.enableJetifier=true
```

## Usage

### Pay with Card

1. Configure the billing & shipping info, the shipping info is optional

```javascript
let billingDetails = new cordova.plugins.CordovaPaymentPlugin.PaymentSDKBillingDetails(name= "John Smith",
                                  email= "email@test.com",
                                  phone= "9731111111",
                                  addressLine= "address line",
                                  city= "Dubai",
                                  state= "Dubai",
                                  countryCode= "ae", // ISO alpha 2
                                  zip= "1234")
let shippingDetails = new cordova.plugins.CordovaPaymentPlugin. PaymentSDKShippingDetails(name= "John Smith",
                                  email= "email@test.com",
                                  phone= "9731111111",
                                  addressLine= "address line",
                                  city= "Dubai",
                                  state= "Dubai",
                                  countryCode= "ae", // ISO alpha 2
                                  zip= "1234")
                                              
```

2. Create object of `PaymentSDKConfiguration` and fill it with your credentials and payment details.

```javascript
let configuration = new cordova.plugins.CordovaPaymentPlugin.PaymentSDKConfiguration();
    configuration.profileID = "*your profile id*"
    configuration.serverKey= "*server key*"
    configuration.clientKey = "*client key*"
    configuration.cartID = "545454"
    configuration.currency = "AED"
    configuration.cartDescription = "Flowers"
    configuration.merchantCountryCode = "ae"
    configuration.merchantName = "Flowers Store"
    configuration.amount = 20
    configuration.screenTitle = "Pay with Card"
    configuration.billingDetails = billingDetails
    configuration.forceShippingInfo = false
```

Options to show billing and shipping info

```javascript
	configuration.showBillingInfo = true
	configuration.showShippingInfo = true
```

# 1- Pay with card
Start payment by calling `startCardPayment` method and handle the transaction details 

```javascript
cordova.plugins.CordovaPaymentPlugin.startCardPayment(configuration, function (result) {
        if (result["status"] == "success") {
            // Handle transaction details here.
            var transactionDetails = result["data"];
            console.log("responseCode:" + transactionDetails.paymentResult.responseCode)
            console.log("transactionTime:" + transactionDetails.paymentResult.transactionTime)
            console.log("responseMessage:" + transactionDetails.paymentResult.responseMessage)
            console.log("transactionReference:" + transactionDetails.transactionReference)
            console.log("token:" + transactionDetails.token)
          } else if (result["status"] == "error") {
            // Handle error here the code and message.
          } else if (result["status"] == "event") {
            // Handle events here.
          }
    }, function (error) {
        console.log(error)
    });
```

<img width="191" alt="card" src="https://user-images.githubusercontent.com/17829232/205496647-59a35cce-4976-423d-9568-d23f4cea91fc.png">


# 2- Pay with Token
Start payment by calling `startTokenizedCardPayment` method and handle the transaction details 

```javascript
cordova.plugins.CordovaPaymentPlugin.startTokenizedCardPayment(configuration,
"Token",
"TransactionReference",
 function (result) {
        if (result["status"] == "success") {
            // Handle transaction details here.
            var transactionDetails = result["data"];
            console.log("responseCode:" + transactionDetails.paymentResult.responseCode)
            console.log("transactionTime:" + transactionDetails.paymentResult.transactionTime)
            console.log("responseMessage:" + transactionDetails.paymentResult.responseMessage)
            console.log("transactionReference:" + transactionDetails.transactionReference)
            console.log("token:" + transactionDetails.token)
          } else if (result["status"] == "error") {
            // Handle error here the code and message.
          } else if (result["status"] == "event") {
            // Handle events here.
          }
    }, function (error) {
        console.log(error)
    });
```

# 3- Pay with 3DS Secured Token
Start payment by calling `start3DSecureTokenizedCardPayment` method and handle the transaction details 

```javascript
let cardInfo = new PaymentSDKSavedCardInfo("Card mask", "cardType")
cordova.plugins.CordovaPaymentPlugin.start3DSecureTokenizedCardPayment(configuration, cardInfo, "token",
function (result) {
        if (result["status"] == "success") {
            // Handle transaction details here.
            var transactionDetails = result["data"];
            console.log("responseCode:" + transactionDetails.paymentResult.responseCode)
            console.log("transactionTime:" + transactionDetails.paymentResult.transactionTime)
            console.log("responseMessage:" + transactionDetails.paymentResult.responseMessage)
            console.log("transactionReference:" + transactionDetails.transactionReference)
            console.log("token:" + transactionDetails.token)
          } else if (result["status"] == "error") {
            // Handle error here the code and message.
          } else if (result["status"] == "event") {
            // Handle events here.
          }
    }, function (error) {
        console.log(error)
    });
```
<img width="197" alt="rec 3ds" src="https://user-images.githubusercontent.com/17829232/205496677-3e22a19e-84f4-4200-8c0d-25b9d153b862.png">


# 4- Pay with saved card
Start payment by calling `startPaymentWithSavedCards` method and handle the transaction details 

```javascript
cordova.plugins.CordovaPaymentPlugin.startPaymentWithSavedCards(configuration, support3DsBool,
function (result) {
        if (result["status"] == "success") {
            // Handle transaction details here.
            var transactionDetails = result["data"];
            console.log("responseCode:" + transactionDetails.paymentResult.responseCode)
            console.log("transactionTime:" + transactionDetails.paymentResult.transactionTime)
            console.log("responseMessage:" + transactionDetails.paymentResult.responseMessage)
            console.log("transactionReference:" + transactionDetails.transactionReference)
            console.log("token:" + transactionDetails.token)
          } else if (result["status"] == "error") {
            // Handle error here the code and message.
          } else if (result["status"] == "event") {
            // Handle events here.
          }
    }, function (error) {
        console.log(error)
    });
```
<img width="197" alt="rec 3ds" src="https://user-images.githubusercontent.com/17829232/205496703-b823e57b-348c-4109-9429-ab261e5a5b50.png">


### Pay with Apple Pay

1. Follow the guide [Steps to configure Apple Pay][applepayguide] to learn how to configure ApplePay with ClickPay.

2. Do the steps 1 and 2 from **Pay with Card** although you can ignore Billing & Shipping details and Apple Pay will handle it, also you must pass the **merchant name** and **merchant identifier**.

```javascript
configuration.merchantApplePayIdentifier = "com.merchant.bundleid"
```

3. To simplify ApplePay validation on all user's billing info, pass **simplifyApplePayValidation** parameter in the configuration with **true**.

```javascript
configuration.simplifyApplePayValidation = true
```

4. Call `startApplePayPayment` to start payment

```javascript
cordova.plugins.CordovaPaymentPlugin.startApplePayPayment(configuration, function (result) {
        if (result["status"] == "success") {
            // Handle transaction details here.
            var transactionDetails = result["data"];
            console.log("responseCode:" + transactionDetails.paymentResult.responseCode)
            console.log("transactionTime:" + transactionDetails.paymentResult.transactionTime)
            console.log("responseMessage:" + transactionDetails.paymentResult.responseMessage)
            console.log("transactionReference:" + transactionDetails.transactionReference)
            console.log("token:" + transactionDetails.token)
          } else if (result["status"] == "error") {
            // Handle error here the code and message.
          } else if (result["status"] == "event") {
            // Handle events here.
          }
    }, function (error) {
        console.log(error)
    });
```

### Pay with Samsung Pay

Pass Samsung Pay token to the configuration and call `startCardPayment`

```javascript
configuration.samsungToken = "token"
```

### Pay with Alternative Payment Methods

It becomes easy to integrate with other payment methods in your region like STCPay, OmanNet, KNet, Valu, Fawry, UnionPay, and Meeza, to serve a large sector of customers.

1. Do the steps 1 and 2 from **Pay with Card**.

2. Choose one or more of the payment methods you want to support.

```javascript
configuration.alternativePaymentMethods = [AlternativePaymentMethod.stcPay]
```

3. Start payment by calling `startAlternativePaymentMethod` method and handle the transaction details 

```javascript

cordova.plugins.CordovaPaymentPlugin.startAlternativePaymentMethod(configuration, function (result) {
        if (result["status"] == "success") {
            // Handle transaction details here.
            var transactionDetails = result["data"];
            console.log("responseCode:" + transactionDetails.paymentResult.responseCode)
            console.log("transactionTime:" + transactionDetails.paymentResult.transactionTime)
            console.log("responseMessage:" + transactionDetails.paymentResult.responseMessage)
            console.log("transactionReference:" + transactionDetails.transactionReference)
            console.log("token:" + transactionDetails.token)
          } else if (result["status"] == "error") {
            // Handle error here the code and message.
          } else if (result["status"] == "event") {
            // Handle events here.
          }
    }, function (error) {
        console.log(error)
    });
     
```

## Enums

Those enums will help you in customizing your configuration.

* Tokenise types

 The default type is none

```javascript
exports.TokeniseType = Object.freeze({
"none":"none", // tokenise is off
"merchantMandatory":"merchantMandatory", // tokenise is forced
"userMandatory":"userMandatory", // tokenise is forced as per user approval
"userOptinoal":"userOptional" // tokenise if optional as per user approval
});
```

```javascript
configuration.tokeniseType = cordova.plugins.CordovaPaymentPlugin.TokeniseType.userOptinoal
```

* Token formats

The default format is hex32

```javascript
exports.TokeniseFromat = Object.freeze({"none":"1", 
"hex32": "2", 
"alphaNum20": "3", 
"digit22": "3", 
"digit16": "5", 
"alphaNum32": "6"
});
```

```javascript
configuration.tokeniseFormat = cordova.plugins.CordovaPaymentPlugin.TokeniseFromat.hex32
```

* Transaction types

The default type is sale

```javascript
const TransactionType = Object.freeze({"sale":"sale", 
"authorize": "auth"});
```

```javascript
configuration.transactionType = cordova.plugins.CordovaPaymentPlugin.TransactionType.sale
```

* Alternative payment methods

```javascript
AlternativePaymentMethod = Object.freeze({"unionPay":"unionpay", 
"stcPay":"stcpay", 
"valu": "valu", 
"meezaQR": "meezaqr", 
"omannet": "omannet", 
"knetCredit": "knetcredit", 
"knetDebit": "knetdebit", 
"fawry": "fawry"});
 ```
 
 ```javascript
configuration.alternativePaymentMethods = [cordova.plugins.CordovaPaymentPlugin.AlternativePaymentMethod.stcPay, ...]
 ```

## Demo application

Check our complete [sample](https://github.com/clickpaysa/clickpay-cordova/tree/master/sample).


## Overriding Resources:

to override fonts Please add your custom fonts files with these names

payment_sdk_primary_font.tff && payment_sdk_secondary_font.tff

to override strings, colors or dimens add the resource you need to override from below resources
with the value you want

## Theme

Use the following guide to customize the colors, font, and logo by configuring the theme and pass it
to the payment configuration.

![UI guide](https://user-images.githubusercontent.com/95287975/160391259-97aaff10-cb9f-4103-bc3e-a938a1111128.png)

## Override strings

To override string you can find the keys with the default values here
[english]( https://github.com/clickpaysa/clickpay-android-library-sample/blob/master/res/strings.xml)
[arabic](https://github.com/clickpaysa/clickpay-android-library-sample/blob/master/res/strings-ar.xml)

````xml

<resourse>
    // to override colors
    <color name="payment_sdk_primary_color">#5C13DF</color>
    <color name="payment_sdk_secondary_color">#FFC107</color>
    <color name="payment_sdk_primary_font_color">#111112</color>
    <color name="payment_sdk_secondary_font_color">#6D6C70</color>
    <color name="payment_sdk_separators_color">#FFC107</color>
    <color name="payment_sdk_stroke_color">#673AB7</color>
    <color name="payment_sdk_button_text_color">#FFF</color>
    <color name="payment_sdk_title_text_color">#FFF</color>
    <color name="payment_sdk_button_background_color">#3F51B5</color>
    <color name="payment_sdk_background_color">#F9FAFD</color>
    <color name="payment_sdk_card_background_color">#F9FAFD</color>

    // to override dimens
    <dimen name="payment_sdk_primary_font_size">17sp</dimen>
    <dimen name="payment_sdk_secondary_font_size">15sp</dimen>
    <dimen name="payment_sdk_separator_thickness">1dp</dimen>
    <dimen name="payment_sdk_stroke_thickness">.5dp</dimen>
    <dimen name="payment_sdk_input_corner_radius">8dp</dimen>
    <dimen name="payment_sdk_button_corner_radius">8dp</dimen>

</resourse>
````


## See the common issues from here

[common issues](https://github.com/clickpaysa/clickpay-android-library-sample/blob/main/common_issues.md)

## Notes

1- Please configure the IPN to avoid loosing any of the transaction status.


## License

See [LICENSE][license].

## ClickPay

[Support][1] | [Terms of Use][2] | [Privacy Policy][3]

 [1]: https://clickpay.freshdesk.com/en/support/solutions
 [2]: https://clickpay.com.sa/wps/portal/clickPay/clickpay/footerpages/termsandconditions
 [3]: https://clickpay.com.sa/wps/portal/clickPay/clickpay/footerpages/privacy
 [license]: https://github.com/clickpaysa/clickpay-ios-library-sample/blob/main/LICENSE

