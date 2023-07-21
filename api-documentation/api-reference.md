---
description: >-
  Documentation for API V2. Major update is addresses with exchange crypto to
  fiat and vice versa abilities.
---

# API Reference

## General information

API endpoint for all requests in production environment is:

```
https://app.cryptoprocessing.com/api/v2
```

API endpoint for all requests in test environment is:

```
https://app.sandbox.cryptoprocessing.com/api/v2
```

#### Deposit flow

1. You obtain new address from CoinsPaid API (for some currencies it may be address and tag) and store it somewhere on your side. After that you show this address to your customer in order to make a deposit.
2. Customer sends some funds to this address. &#x20;
3. When transaction is sent by a customer - CoinsPaid sends a callback to your callback url with transaction details. It contains status, address, currency, amount and fees. \
   If status is successful, you should deposit respective amount to customer balance on your side.

#### Withdrawal flow

1. You request to send amount of money to address.
2. Your request is validated on our side. If signature is correct, address is valid and you have enough balance - CoinsPaid responds you with the transaction object.
3. You will receive a callback when transaction status is updated.

{% hint style="warning" %}
Please note that the final status and all calculations on your side shall be applied only after receiving a final callback from Cryptoprocessing's side, hence in case a connection disruption takes place and you do not see a transaction on your side, kindly wait for a final callback or check a transaction in the back-office.
{% endhint %}

**Deposit with exchange flow**

You don't want to touch or store cryptocurrency, but only use it as a payment method. Your customer deposits **BTC**, Coinspaid instantly converts it to **EUR** so that **you would receive EUR on your CoinsPaid account.**

1. You obtain new address from CoinsPaid API same as in deposit flow, but additionally pass another parameter "convert\_to" in your request specifying resulting currency.
2. When new deposit is arriving, CoinsPaid converts all arriving funds to destination funds, and sends notifications as in regular deposit

**Withdrawal with exchange flow**

You wish to send Cryptocurrency from your Fiat currency balance. For example you want to **send EUR amount** but your customer receives money **in BTC.**

1. You do exactly same as in withdrawals, but you specify 2 currencies. One is a currency of your **sending balance** and Second is a **cryptocurrency your Customer wishes to receive**.
2. Your request is validated on our side. If signature is correct, address is valid and you have enough balance - CoinsPaid responds you with the transaction object.
3. You will receive a callback when transaction status is updated.

#### **Invoice flow**

Invoices allow to conduct deposits with a fixed rate within a limited period of time disregarding the exchange rate fluctuations. In case it’s necessary to convert funds in fiat currency or convert it to another crypto currency this option will allow to visualize the exact amount of a sender’s currency required to receive the exact amount in a receiver’s currency. When a deposit is processed through this flow, a user is being redirected to the respective Invoice page via the preset link and just needs to follow instructions specified on it. It also allows to conduct refunds in case a user fails to manage to deposit within an established timeframe or discovers non-sufficient balance. All is required in that case is to follow the link with the respective instructions sent to an e-mail of a customer. \
Detailed information can be found [here](../integration-guide/invoices.md).

## API Endpoints

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/ping" method="get" summary="Ping" %}
{% swagger-description %}
Test if API is up and running and your authorization is working
{% endswagger-description %}

{% swagger-response status="200" description="" %}
```
OK
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
Body must be a valid json object or array, example: {}
{% endhint %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/currencies/list" method="post" summary="Get list of supported currencies" %}
{% swagger-description %}
Get a list of all supported currencies
{% endswagger-description %}

{% swagger-parameter in="body" name="visible" type="boolean" %}
Allows to get a list of currently enabled/disabled currencies 
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
  "data": [
    {
      "id": 1,
      "type": "crypto",
      "currency": "BTC",
      "minimum_amount": "0.001",
      "deposit_fee_percent": "0.99",
      "withdrawal_fee_percent": "0",
      "precision": 8
    }
  ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/currencies/pairs" method="post" summary="Get list of exchangeable currency pairs" %}
{% swagger-description %}
Get list of currency exchange pairs.
{% endswagger-description %}

{% swagger-parameter in="body" name="currency_from" type="string" %}
Filter by currency ISO that exchanges from, example: 

**BTC**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency_to" type="string" %}
Filter by currency ISO that can be converted to, example: 

**EUR**
{% endswagger-parameter %}

{% swagger-response status="200" description="Example of success response" %}
```
{
  "data": [
    {
      "currency_from": {
        "currency": "BTC",
        "type": "crypto",
        "min_amount": "0.00300000",
        "min_amount_deposit_with_exchange": "0.00010000"
      },
      "currency_to": {
        "currency": "EUR",
        "type": "fiat"
      },
      "rate_from": "1",
      "rate_to": "8795.80000000"
    },
    {
      "currency_from": {
        "currency": "EUR",
        "type": "fiat",
        "min_amount": "25.00000000"
      },
      "currency_to": {
        "currency": "BTC",
        "type": "crypto"
      },
      "rate_from": "1",
      "rate_to": "8885.72951839"
    },
    {
      "currency_from": {
        "currency": "BCH",
        "type": "crypto",
        "min_amount": "0.00020000",
        "min_amount_deposit_with_exchange": "0.00100000"
      },
      "currency_to": {
        "currency": "USD",
        "type": "fiat"
      },
      "rate_from": "1",
      "rate_to": "332.28264751"
    },
    {
      "currency_from": {
        "currency": "USD",
        "type": "fiat",
        "min_amount": "30.00000000"
      },
      "currency_to": {
        "currency": "BCH",
        "type": "crypto"
      },
      "rate_from": "1",
      "rate_to": "335.94361522"
    }
  ]
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Example of response with errors" %}
```
{
    "errors": {
        "currency_from": "The selected currency from is invalid.",
        "currency_to": "The selected currency to is invalid."
    }
}
```
{% endswagger-response %}
{% endswagger %}



{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/currencies/rates" method="post" summary="Get list of currencies rates" %}
{% swagger-description %}
Get a particular pair and its price.
{% endswagger-description %}

{% swagger-parameter in="path" name="currency_from" type="string" %}
Filter by currency ISO that exchanges from,

\


example: 

**BTC**
{% endswagger-parameter %}

{% swagger-parameter in="path" name="currency_to" type="string" %}
Filter by currency ISO that can be converted to, example: 

**EUR**
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "data": [
        {
            "currency_from": {
                "currency": "BTC",
                "type": "crypto",
                "min_amount": "0.00010000",
                "min_amount_deposit_with_exchange": "0.00010000"
            },
            "currency_to": {
                "currency": "EUR",
                "type": "fiat"
            },
            "rate_from": "1",
            "rate_to": "48715.61680000"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/accounts/list" method="post" summary="Get list of balances" %}
{% swagger-description %}
Get list of all the balances (including zero balances).
{% endswagger-description %}

{% swagger-response status="200" description="" %}
```
{
    "data": [
        {
            "currency": "DOGE",
            "type": "crypto",
            "balance": "13234.91276375"
        },
        {    
            "currency": "ADA",
            "type": "crypto",
            "balance": "7272.36400468"
        },
        {
            "currency": "EUR",
            "type": "fiat",
            "balance": "5973.97568920"
        },
        {
            "currency": "USDT",
            "type": "crypto",
            "balance": "0.00000000"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/addresses/take" method="post" summary="Receive cryptocurrency" %}
{% swagger-description %}
Take address for depositing crypto and (it depends on specified params) exchange from crypto to fiat on-the-fly.
{% endswagger-description %}

{% swagger-parameter in="body" name="foreign_id" type="string" %}
Your info for this address, will returned as reference in Address responses, example: 

**user-id:2048**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" %}
ISO of currency to receive funds in, example: 

**BTC**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="convert_to" type="string" %}
If you need auto exchange all incoming funds for example to 

**EUR**

, specify this param as EUR or any other supported currency ISO, to see list of pairs see previous method.
{% endswagger-parameter %}

{% swagger-response status="201" description="Example of success response" %}
```
{
  "data": {
    "id": 1,
    "currency": "BTC",
    "convert_to": "EUR",
    "address": "12983h13ro1hrt24it432t",
    "tag": tag-123,
    "foreign_id": "user-id:2048"
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Example of response with errors" %}
```
{
    "errors": {
        "foreign_id": "The foreign id field is required."
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% hint style="info" %}
Business logic for using cryptocurrency as a deposit method: \
You are willing to let your customer fund his EUR balance on your platform or website. You will have to generate an address in the desired cryptocurrency and specify EUR as a "convert\_to" currency. This will allow you to let your Customer pay if his favorite currency and fund his balance in EUR. At the same time you will see respective EUR amount in your CoinsPaid merchant account.\
**Hint:** you don't have to generate new address for this customer anymore, address can be reused unlimited amount of times.
{% endhint %}

![Example of the customer facing interface for Deposits. ](../.gitbook/assets/QR\_API\_2.png)

* Make sure to use Bitcoin URI format bitcoin: in QR. Works the same way as "mailto:".
* We do recommend making this QR clickable as customers may have a wallet set up on their computer or mobile phone.
* We recommend specifying approximate current exchange rate.

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/withdrawal/crypto" method="post" summary="Withdraw cryptocurrency" %}
{% swagger-description %}
Withdraw in crypto to any specified address. You can send Cryptocurrency from your Fiat currency balance by using "convert_to" parameter. 
{% endswagger-description %}

{% swagger-parameter in="body" name="foreign_id" type="string" %}
Unique foreign ID in your system, example: "

**122929**

"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" %}
Amount of funds to withdraw, example: 

**"1"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" %}
Currency ISO to be withdrawn, example: "

**BTC**

"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="convert_to" type="string" %}
If you want to auto convert for example EUR to BTC, specify this param as 

**BTC**

 or any other currency supported (see list of exchangeable pairs API method).
{% endswagger-parameter %}

{% swagger-parameter in="body" name="address" type="string" %}
Cryptocurrency address where you want to send funds.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="tag" type="string" %}
Destination tag/memo (if it’s Ripple or BNB).
{% endswagger-parameter %}

{% swagger-response status="201" description="Example of success response of withdraw without conversion" %}
```
{
  "data": {
    "id": 1,
    "foreign_id": "122929",
    "type": "withdrawal",
    "status": "processing",
    "amount": "0.01000000",
    "sender_amount": "0.01000000",
    "sender_currency": "ETH",
    "receiver_amount": "0.01000000",
    "receiver_currency": "ETH"
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Example of response with errors" %}
```
{
  "errors": {
    "amount": "The amount must be at least 0.001."
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/exchange/calculate" method="post" summary="Calculate exchange rates" %}
{% swagger-description %}
Get info about exchange rates.

\




\


Please note, this endpoint has limitation 

**up to 30 requests per minute**

 from one IP address, in case this amount is exceeded a new successful response can only be obtained after one minute break.
{% endswagger-description %}

{% swagger-parameter in="body" name="receiver_amount" type="string" %}
Amount you want to calculate for getting, example: 

**"10".**

 The parameter is required when the "sender_amount" parameter is absent
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender_currency" type="string" %}
Currency ISO for which you want to calculate the exchange rate, example: 

**"BTC"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receiver_currency" type="string" %}
Currency ISO to be exchanged, example: 

**"EUR"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender_amount" type="string" %}
Amount you want to calculate, example: 

**"3".**

 The parameter is required when the "receiver_amount" parameter is absent
{% endswagger-parameter %}

{% swagger-response status="200" description="Example of success response" %}
```
{
  "data": {
    "sender_amount": 1,
    "sender_currency": "BTC",
    "receiver_amount": "8549.81680000",
    "receiver_currency": "EUR",
    "fee_amount": "85.49816800",    
    "fee_currency": "BTC",
    "price": "8549.81680000",
    "ts_fixed": 1564293159,
    "ts_release": 1564293219,
    "fix_period": 60
  }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Example of response with errors" %}
```
{
  "errors": {
    "sender_currency": "Exchange is unavailable for given currencies"
  }
}
```
{% endswagger-response %}

{% swagger-response status="429" description="" %}
```
{
  "errors": {
    "error code: 1015"
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/exchange/fixed" method="post" summary="Exchange on fixed exchange rate" %}
{% swagger-description %}
Make exchange on a given fixed exchange rate.
{% endswagger-description %}

{% swagger-parameter in="body" name="sender_currency" type="string" %}
Currency ISO which you want to exchange, example: 

**"LTC"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receiver_currency" type="string" %}
Currency ISO to be exchanged, example: 

**"USD"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender_amount" type="string" %}
Amount you want to exchange, example: 

**"6.5"**

\


**Please note:**

\


That this value shall be the same as the value specified in the exchange/calculate request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="foreign_id" type="string" %}
Unique foreign ID in your system, example: 

**"134453"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="string" %}
Exchange rate price on which exchange will be placed, example: 

**"89.75202000"**
{% endswagger-parameter %}

{% swagger-response status="201" description="Example of success response" %}
```
{
  "data": {
     "id": 2687667,
     "foreign_id": "knwi24op9",
     "type": "exchange",
     "sender_amount": "0.01",
     "sender_currency": "BTC",
     "receiver_amount": "63.52069015",
     "receiver_currency": "EUR",
     "fee_amount": "6.98727592",
     "fee_currency": "EUR",
     "price": "6352.06901520",
     "status": "processing"
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/exchange/now" method="post" summary="Exchange regardless the exchange rate " %}
{% swagger-description %}
Make exchange without mentioning the price.
{% endswagger-description %}

{% swagger-parameter in="body" name="sender_currency" type="string" %}
Currency ISO which you want to exchange, example: 

**"EUR"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="receiver_currency" type="string" %}
Currency ISO to be exchanged, example: 

**"BTC"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender_amount" type="string" %}
Amount you want to exchange, example: 

**"2"**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="foreign_id" type="string" %}
Unique foreign ID in your system, example: 

**"124876"**
{% endswagger-parameter %}

{% swagger-response status="201" description="Example of success response" %}
```
{
  "data": {
     "id": 2687669,
     "foreign_id": "wph27bmsp81",
     "type": "exchange",
     "sender_amount": "0.001",
     "sender_currency": "BTC",
     "receiver_amount": "6.33984642",
     "receiver_currency": "EUR",
     "fee_amount": "0.69738311",
     "fee_currency": "EUR",
     "price": "6339.84642127",
     "status": "processing"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Example of response with errors" %}
```
{
  "errors": {
    "sender_amount": "The amount must be at least 0.00300000 "
  }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://app.cryptoprocessing.com/api" path="/v2/invoices/create" method="post" summary="Create Invoice" %}
{% swagger-description %}
Create invoice for the client for a specified amount.
{% endswagger-description %}

{% swagger-parameter in="body" name="timer" type="boolean" required="true" %}
Time on the rate is fixed for invoice payment (15 minutes). During this time the user has to pay an invoice.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="title" type="string" required="true" %}
Invoice title that will be displayed to the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
There're a couple of sub-types of invoices:

\




\


1\. Standard

\


2\. With partial pay

\




\


In order to create an invoice with partial pay a value of the "type" parameter shall be set to “good_until_expired“

\




\


For standard invoices, the value would be either “fill_or_kill“ or you can avoid using the "type" parameter at all.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="description" type="string" %}
Invoice description that will be displayed to the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currency" type="string" required="true" %}
ISO invoice currency that you want to receive from the user, for example: 

**“EUR”**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sender_currency" type="string" %}
Currency of user invoice payment (3rd type invoice will be externalized at the time of sending this parameter with timer= true), example: 

**“BTC“**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="amount" type="string" required="true" %}
Invoice amount that you want to receive from the user, example: 

**“106.75“**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="foreign_id" type="string" required="true" %}
Unique foreign ID in your system, example: "

**164**

"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url_success" type="string" required="true" %}
URL on which we redirect the user in case of a successful invoice payment, example: 

**“https://merchant.name.com/url_success“**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="url_failed" type="string" required="true" %}
URL on which we redirect the user in case of an unsuccessful invoice payment, example: 

**“https://merchant.name.com/url_failed“**
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email_user" type="string" required="true" %}
In case the payment amount does not match the amount stated above, we will send an email to the stated address with instructions on funds recovery. In case of underpayment, the whole amount will be refunded. In case of overpayment, user will be able to recover the difference by following the instructions
{% endswagger-parameter %}

{% swagger-response status="200" description="Example of a successful response" %}
```
{
   "data":{
      "id":79,
      "url":"https://app.coinspaid.com/invoice/RB9NZv",
      "foreign_id":164,
      "name":"TEST NAME",
      "status":"created",
      "currency":"EUR",
      "amount":"106.75",
      "sender_currency":"BTC",
      "sender_amount":null,
      "fixed_at":1581929889,
      "release_at":1581930789
   }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Examples of a responses with errors" %}
```
{
   "errors":{
      "foreign_id":"The foreign id has already been taken."
   }
};

{
    "errors": {
        "amount": "The amount is too small. The minimum amount is 10.00 EUR."
    }
}
```
{% endswagger-response %}
{% endswagger %}

## Payment terminal JSON parameters

A set of parameter included in URL that will allow to redirect a user to Payment Terminal. For more info navigate through [this section of documentation](../integration-guide/payment-terminal.md).

| **Name**    | **Description**                                                                                                                                                                                       | **Optionality** | **Type** |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | -------- |
| client\_id  | This is a unique ID that’s generated on the side of CoinsPaid                                                                                                                                         | Required        | int      |
| currency    | ISO of a currency to receive funds in, example: **BTC**                                                                                                                                               | Required        | string   |
| amount      | Amount of funds to withdraw, example: "**3500**"                                                                                                                                                      | Optional        | numeric  |
| convert\_to | In case you need on-the-fly exchange of all incoming funds (e.g. to EUR) specify this parameter as EUR or any other supported currency ISO, to see the list of available pairs check the method above | Optional        | string   |
| is\_iframe  | The parameter that allows you to get an iframe-link (false by default).                                                                                                                               | Optional        | boolean  |
| foreign\_id | Unique foreign ID in your system, example: "**164**"                                                                                                                                                  | Required        | string   |
| url\_back   | A link that allows you to get a user back to your system                                                                                                                                              | Optional        | url      |

## Transaction statuses

| Status         | Meaning                                                                                                                                                                           |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| confirmed      | **Final**. You are safe to process this transaction                                                                                                                               |
| not\_confirmed | Transaction is not yet confirmed.                                                                                                                                                 |
| cancelled      | **Final**. This transaction is a double spend or cancelled withdrawal. Pay attention to this transaction.                                                                         |
| pending        | This status may occur only after enabling withdrawal limits. Transaction exceeds set withdrawal limit, you need to confirm or decline it via backoffice of your merchant account. |

## "transaction\_type" parameter values

| Type       | Description                                                                                                                                                                                                                                                                                                                   |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Blockchain | Type of transactions that are written into blockchain. Such transactions (deposits and withdrawals) can be tracked via according explorer for suitable blockchain. This is the most common type of transactions.                                                                                                              |
| Internal   | Type of transactions between two addresses within our processing (between separate merchant accounts or different addresses of the single merchant). Such transactions are not written in blockchain, but still can be tracked via our internal explorer - [https://explorer.coinspaid.com/](https://explorer.coinspaid.com/) |
| Exchange   | Type of transactions that requires exchange between crypto-fiat or crypto-crypto pairs.                                                                                                                                                                                                                                       |

## Transitions

| Transaction             | Transition                  |
| ----------------------- | --------------------------- |
| Successful deposit      | not\_confirmed -> confirmed |
| Unsuccessful deposit    | not\_confirmed -> cancelled |
| Successful withdrawal   | confirmed                   |
| Unsuccessful withdrawal | cancelled                   |
