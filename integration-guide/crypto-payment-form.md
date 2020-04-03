---
description: How to increase the payment form conversion rate and total turnover
---

# What is crypto payment form?

## Introduction <a id="QRcodeimplementation-Introduction"></a>

Among the best practices of working with cryptocurrencies there are some recommendations on how to increase the payment form conversion rate and total turnover.

As you may know, a payment form for crypto payments differs from classic payment methods. Users can send their funds using exchanges and crypto wallet applications instead of classic payment forms. Crypto payment form is a block with the information about payment conditions and crypto address where funds should be sent. The main idea is to provide a user with a deposit crypto address and all necessary information about deposit limits, exchange rates and other payment conditions. Also it will be a good idea to provide crypto addresses using QR codes that users can use as an automatic way to open their wallet application and send a cryptocurrency in one click.

The most important features of using QR codes are:

1. Quick access from mobile devices
2. Predefined cryptocurrency 
3. An integrated clickable link that opens the wallet application

Optional features are:

1. Predefined amounts
2. Inline comments with the payment description

In this section you will learn how to provide the user with all the necessary information, how to implement QR codes to your payment form and what best practices exist in order to make the payment form user friendly, to increase its conversion rate and to avoid user mistakes.

## What is a crypto wallet URI format? <a id="QRcodeimplementation-WhatisacryptowalletURIformat?"></a>

Almost every PC user uses email links on websites. Usually such links have the following format:

[address@email.com](mailto:address@email.com)\*\*\*\*

{% hint style="info" %}
**mailto**:address@email.com
{% endhint %}

When one clicks the link an email client will be opened automatically. The user will see the form for composing a new email that contains a recipient email address in the field "To". In other cases different fields like the field "Subject" will contain the data too.

The same user-friendly way of interaction can be used with the crypto wallets too. BTC link has the following format:

{% hint style="info" %}
**bitcoin**:3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W
{% endhint %}

If the user has a wallet application on their device and follows this link, wallet application will open with the specified address. In this case the user should make only one action to click a "Pay" button in order to proceed with the payment.

BTC URI supports not only the address but also other options, for example, a payment amount.

{% hint style="info" %}
BTC URI has a special standard "BIP-0021" described here:

[https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki](https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki)
{% endhint %}

## Why should you present a crypto address as a clickable link instead of text string? <a id="QRcodeimplementation-WhyshouldIpresentacryptoaddressasaclickablelinkinsteadoftextstring?"></a>

The most common way to provide a crypto address for a user is to show their the address as a text string:

{% hint style="info" %}
"Please, make a deposit using the following BTC address: **3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W**"
{% endhint %}

If the user has the crypto wallet application on the same device, they should:

1. Copy this address to the clipboard
2. Find and open their crypto wallet application
3. Open the "Withdraw" section in the application
4. Paste the crypto address
5. Click a "Send" button to transfer their funds

{% hint style="danger" %}
The more actions a user has to ****make the more probable it is that they will not pay. That is why **the crypto address has to be presented at least as a clickable link** using a specific URI format \(see the [What is a crypto wallet URI format?](https://docs.coinspaid.com/docs/faq/qr-codes-implementation#QRcodeimplementation-WhatisacryptowalletURIformat?) section\).
{% endhint %}

## What is a QR code? <a id="QRcodeimplementation-WhatisaQRcode?"></a>

A QR code \(Quick Response code\) is a special visual method of data encoding and transferring that is usually used for simple and fast semi-automatic interaction with users' mobile devices. It can contain any text data, including URL links. When the user uses their phone to scan the QR code, the data inside the QR code will be decoded. If it is a link associated with a special application, the user's smartphone will react in a predefined way. For example, it can suggest to the user to follow the URL using a web browser or to send the funds using their crypto wallet application.

An example of QR code:

![](../.gitbook/assets/image%20%2811%29.png)

## Why should I use QR codes on my payment form? <a id="QRcodeimplementation-WhyshouldIuseQRcodesonmypaymentform?"></a>

As it was described above, the user has to follow the 5 steps in order to make a deposit if they use a web browser and a crypto wallet on the same device. That is why the address should be presented as a link instead of a text string.

But imagine now that a user gets to a page with the payment form using their laptop and their crypto wallet application is installed on the user's smartphone.

{% hint style="danger" %}
At worst, the only way for the user to pay is to type every symbol from the address manually; the most likely outcome is that the user will leave the form without the deposit. **That is why the QR code with the crypto address should be used at the same time as a link.**
{% endhint %}

## How to create QR code <a id="QRcodeimplementation-HowtocreateQRcode"></a>

In order to provide the best user experience you only need to encode into the QR code a simple URI with the crypto address inside.

The simplest way to create a QR code is to use Google Chart Service. It is a special service that generates universal QR codes and has a very simple API to manage it. According to the request parameters the QR code will contain the necessary data and it will have defined size dimensions.

A minimum set of parameters is:  
**chs** - chart image size  
**cht** - chart type \(**"qr" is necessary for QR code**\)  
**chl** - the data encoded in your QR code  
**choe** - encoding type of the QR code data

{% hint style="info" %}
Detailed description can be found here:  
[https://developers.google.com/chart/infographics/docs/qr\_codes](https://developers.google.com/chart/infographics/docs/qr_codes)
{% endhint %}

In order to create the QR code you can use Google Chart Service and encode the URI described in [What is a crypto wallet URI format?](https://docs.coinspaid.com/docs/faq/qr-codes-implementation#QRcodeimplementation-WhatisacryptowalletURIformat?) section.

To create simple QR codes including the link to the bitcoin address the following parameters should be used:  
[https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=bitcoin:3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W&choe=UTF-8](https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=bitcoin:3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W&choe=UTF-8)

You can use this link directly inside the &lt;img&gt; tag:

```markup
<img src="https://chart.googleapis.com/chart?chs=150x150&cht=qr&chl=bitcoin:3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W&choe=UTF-8">
```

![](../.gitbook/assets/image%20%2818%29.png)

**chs** - QR code size \("150x150" size is used as an example\)  
**cht** - chart type \(**"qr" is necessary for QR code**\)  
**chl** - the data encoded in the QR code \("bitcoin:3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W" has been used in the example above, but additional parameters can be used according to "BIP-0021" standard documentation: [https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki](https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki)\)  
**choe** - encoding type of the QR code data \("UTF-8" is required by "BIP-0021" standard\)

When the user scans this QR code they will be able to open the wallet application and to make the deposit in one click.

## Best practice as a result <a id="QRcodeimplementation-Bestpracticeasaresult"></a>

This article described how to increase the conversion rate and as a result total turnover of the payment form for two scenarios. To be sure that the users will have a good experience in both cases all you need is to combine these two methods and use them on the payment form at the same time.

**So, the last step is to make the QR code clickable.**

```markup
<a href="bitcoin:3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W" target="_blank">
  <img src="https://chart.googleapis.com/chart?chs=150x150&amp;cht=qr&amp;chl=bitcoin:3AFaCnqriLNxj15kqtp5Pxn8puHfuqbX7W&amp;choe=UTF-8">
</a>
```

After that it is doesn't matter whether the user gets the payment by using their laptop or smartphone. They get the possibility to make simple and fast payments in one click without any inconveniences.

To make this experience even better, it will be a good idea to provide the payment form with:

* clickable QR code
* crypto address as a link
* current or approximate exchange rate
* minimal deposit limit
* warning about the cryptocurrency that should be used with the specified address

As a result created form may look like this:

![](../.gitbook/assets/deposit-or-bitstarz.com-2019-10-04-15-31-35.png)



