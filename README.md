# <img align="center" src="./docs/img/polyright-icon.png" height="64">  polyright Payment Terminal - URI Scheme Integration

The polyright PaymentTerminal application allows payments on any polyright system through the polyright platform. The application is available for desktop, tablet and smartphone.

<br>

## Getting Started

### Prerequisites
- RFID or NFC reader
- Internet connection
- Compatible platforms:
  - Windows 10.0.10240
  - Windows Mobile 10.0.586
  - Android 4.4
  - iOS 11 *(coming soon)*

### Installation
1. Install application from App Store
    * [Windows Store](https://www.microsoft.com/store/p/polyright-payment-terminal/9nblggh5263v)
    * [Google Play](https://play.google.com/store/apps/details?id=com.polyright.PaymentTerminal)
    * Apple Store *(coming soon)*
2. Launch application
3. Activate Payment Terminal
4. Ready!

<br>

## Integration
URI Scheme is supported by Payment Terminal to allow simplified integration of polyright payment from other applications and websites.
For full integration and best user experience, use the REST API and CardReader SDK provided by polyright.

### Supported URI Schemes
| URI Scheme                   | Description                       |
|------------------------------|-----------------------------------|
| `pay://transaction`          | Start a new transaction          |
| `pay://transaction/validate` | Validate the current transaction |
| `pay://transaction/cancel`   | Cancel the current transaction   |

###### Parameters
| Parameters           | Description                                                                                                                                                                                                                            |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `amount`             | Amount with point as decimal separator                                                                                                                                                                                                 |
| `purpose`            | Transaction description for the end user                                                                                                                                                                                               |
| `externalId`         | Your transaction ID. This must be unique                                                                                                                                                                                               |
| `paymentMode`        | Mode of payment. Null for all supported modes.<br>  Supported modes: `Epurse`, `Twint`                                                                                                                                                 |
| `validationCallback` | URI Scheme called to validate transaction when person was found. This allows you to apply a discount before processing the transaction by Payment Terminal.<br> The properties of the person are added as Query String of the URI Scheme |
| `successCallback`    | URI Scheme called when the transaction was successfully processed                                                                                                                                                                      |
| `cancelCallback`     | URI Scheme called when the transaction was cancelled                                                                                                                                                                                   |
| `errorCallback`      | URI Scheme called when an error occurred while processing the transaction                                                                                                                                                              |

<br>

### Callback Support
Callbacks are used to send the result of operations to calling applications. 
This can be a URI Scheme of an application or a URL of a web page. 
The results are passed in Query String of URI.

###### How to support URI Scheme in your application?
* [Windows Desktop Aplication](https://msdn.microsoft.com/en-us/library/aa767914(v=vs.85).aspx)
* [Windows 10 UWP Application](https://docs.microsoft.com/en-us/windows/uwp/launch-resume/handle-uri-activation)
* [Android Application](https://developer.android.com/training/basics/intents/filters.html)
* [iOS Application](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html)

<br>

### Examples
- Launch basic transaction: <br>
`pay://transaction?amount=4.25&successCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?success&cancelCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?cancel&errorCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?error`
- Launch transaction with Twint payment mode only: <br>
`pay://transaction?amount=4.25&paymentMode=Twint&successCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?success&cancelCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?cancel&errorCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?error`
- Launch transaction with validation: <br>
`pay://transaction?amount=4.25&paymentMode=Twint&validationCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?validation&successCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?success&cancelCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?cancel&errorCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?error`
- Validate current transaction: <br>
`pay://transaction/validate?amount=4.25&paymentMode=Twint&successCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?success&cancelCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?cancel&errorCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?error`
- Cancel current transaction: <br>
`pay://transaction/cancel?successCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?success&cancelCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?cancel&errorCallback=https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html?error`

<br>

## Samples

### HTML
This simple web page shows how to start a transaction and receive the result from the callback URL<br>

* <a href="https://polyright.github.io/PaymentTerminal-URI-Scheme/samples/html/basic.html">Launch Sample</a>
* [Show source code](https://github.com/polyright/PaymentTerminal-URI-Scheme/blob/master/samples/html/basic.html)
