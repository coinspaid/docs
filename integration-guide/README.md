# Integration guide

## Intro

When we are talking about cryptocurrencies as a payment method, we should keep in mind that its payment workflow differs from classic payment methods like bank cards or e-wallets. As a result, when a client is using this payment method in a web-service or application, they should know some tips on how to make the payment process comfortable and simple.

In this section we would like to share our knowledge of how to work with cryptocurrencies efficiently. We will also describe the most important information about implementation scenarios of Coinspaid API.

## Deposits

Crypto deposits are similar to bank transfers. If the recipient’s bank account number is known then the funds can be directly sent at any time. This approach differs from classic payment methods because the transaction cannot be created before the funds have appeared in the bank account. The same way web-services cannot expect that crypto deposit transactions will be initiated from the "payment form" every time because, in general, there is no such term for cryptocurrencies. Unlike the classical approach, web-services should handle callbacks from payment providers with information about received deposits. When web-services receive the first callback they then ****create the transaction. After the transaction will be confirmed by the payment provider the second callback will inform the web-services about the status of the transaction. Then, web-services can provide the user with a specific service.

{% hint style="warning" %}
#### Attention!

When a user gets an address for the first time they are able to save it into their crypto wallet application. It is more comfortable for the user because they don’t need to go to the "Cashier" section every time when they want to make a deposit. That is why many users save the address in their crypto wallet application after the first deposit and then they don't need to go to the payment form every time.

As cryptocurrencies are based on the blockchain technology, you cannot delete the address if it has already been created and has been written into the blockchain.

If the user knows this address they can always send the funds there, because it is not necessary for the user to interact with the payment form when they would like to send the funds.

Even if you show the users new addresses every time, they can always make the deposit to the older one, and they expect that they will be able to see their funds on your website. 
{% endhint %}

### Common deposit workflow

The most common ****scenario for receiving cryptocurrency is "deposit with exchange". Coinspaid provides web-services with on-the-fly exchange solution. It means that all funds that were received from the users can be automatically converted into fiat currencies in order to avoid cryptocurrency fluctuations and exchange rate inconsistencies.

In case of regular deposits without exchange the workflow there will be the same but the conversion option will be skipped.

> #### Algorithm
>
> 1. User has EUR balance on your site
> 2. User uses some kind of “deposit” option on your site and chooses BTC as a payment method to use for the payment
> 3. Website shows a deposit BTC address to the user
> 4. User scans QR code or copies the address and goes to their crypto wallet application
> 5. When user sends BTC to this address our system makes an automatic exchange of received funds from BTC to EUR and your system gets the callback with the information about the deposit, including transaction's status, currency pairs, amount, fees and so on
> 6. You add the amount from the callback to user’s EUR balance

{% hint style="danger" %}
When you show a deposit address to a user, it is important to notify ****the user about exchange rates, deposit limits and the chosen cryptocurrency. Besides this you may want to warn the user that:

* all deposits below the limits or sent to incorrect addresses will be lost

Here you can find information about deposit and withdrawal limits:

* [Deposit and withdrawal limits](../confirmations-and-limits.md)

Sometimes users make mistakes and send the funds using a specific cryptocurrency to the address from a different blockchain. These funds will be lost in most cases. The funds could be particularly restored according to the "Crosschain recovery policy":

* [Crosschain recovery policy](../crosschain-recovery-policy.md)
{% endhint %}

In order to increase the conversion rate for crypto payments we have a special guide for how you can develop your payment form and provide the user with the best experience of crypto payments. There are good recommendations on how to build friendly and comfortable interactions with your interface for the user. Here you can find out how it can be implemented:

{% page-ref page="crypto-payment-form.md" %}

{% hint style="info" %}
#### Hint 1

Usually our merchants generate all the needed crypto addresses at the time ****when a new user is created. In order to do this you should use the **"/v2/addresses/take"** method from our API.  
You can define what currency should be used for receiving the funds from the user and, if necessary, into what fiat currency received funds should be converted.

In most cases it is useful to send us your user's ID as a **"foreign\_id"** parameter. We will link it to the address and send it in the callbacks. Using such a method you will be able to understand which user made the deposit.
{% endhint %}

{% hint style="warning" %}
#### Attention

Some cryptocurrencies require additional parameters to be defined when a user makes a deposit. For example, users have to input a value into the **"Memo"** field when they make a deposit from their wallet application using **XRP, BNB** or another cryptocurrency as the payment method.

If it is necessary for a specific currency, we send the parameter **"tag"** in the response on **"/v2/addresses/take"** API call. If your system gets this parameter it has to show it's value to the user. In other cases received funds will be lost.
{% endhint %}

{% hint style="info" %}
#### Hint 2

In order to get the information about current exchange rates for different currencies you can use the **"/v2/currencies/pairs"** API method.

If you need to calculate exact amounts corresponding to current exchange rates try the **"/v2/exchange/calculate"** method.
{% endhint %}

{% hint style="info" %}
#### Hint 3

In case you would like to hold the exchange rate for 10 minutes in order to receive a specified amount from the user after converting the funds, you may want to use these methods: **"/v2/futures/rates"** + **"/v2/futures/confirm"**
{% endhint %}

{% hint style="info" %}
#### Hint 4

As we keep a small amount of incoming funds as our fees, we provide you with the information about the fees in the callback.  
It is your choice what amount you will add to user's balance - including fees or not.  
{% endhint %}

## Withdrawals

To the opposite of deposits, sending cryptocurrencies to the users is similar to classic payment methods. Users fill the form where they provide the address and the amount of the withdrawal. After that the web-service creates the transaction and sends a withdrawal request to the payment provider. When the transaction is confirmed by the payment provider, the web-service decreases the user's balance on the website.

### Common withdrawal workflow

The most common scenario for sending crypto is "withdrawal with exchange". Coinspaid provides web-services with on-the-fly exchange solution. This means that the funds that are stored on a merchant's fiat balance can be automatically converted into cryptocurrencies before being sent to the user's crypto wallet.

In case of regular withdrawals without exchange the workflow will be the same except of conversion operation.

> #### Algorithm
>
> 1. You have EUR balance in our system
> 2. User wants to get a withdrawal from their EUR balance on your site to their BTC wallet
> 3. User uses some kind of “withdrawal” option on your site, chooses BTC as the currency to use for the payout and fills the payout form with their BTC address where they want to receive the funds and the withdrawal amount.
> 4. After that your system makes the request to our processing.
> 5. Our system makes an automatic exchange from EUR to BTC, sends funds to the user’s crypto address and your system gets the callback with transaction parameters, including the transaction's status, currency pairs, amount, fees and so on.
> 6. You decrease the user's EUR balance for the transaction amount

{% hint style="info" %}
#### Hint 5

In order to make a withdrawal you should use the **"/v2/withdrawal/crypto"** method from our API.  
You can define what currency should be used to send the funds, and, if necessary, from what fiat currency the funds should be converted before sending to the user.
{% endhint %}

{% hint style="warning" %}
#### Attention

Unlike the "**/v2/addresses/take**" method, you should use the unique "foreign\_id" every time you make a withdrawal request to our system. 
{% endhint %}

## Callbacks

Every time a user makes a deposit or our system sends a withdrawal into the blockchain, you will receive the callback. Callbacks contains all the important information about the transaction:

* status
* currency
* amount
* blockchain transaction's hash
* address
* fees
* number of confirmations
* ...and so on

{% hint style="warning" %}
#### Attention

As our system supports instant confirmations it means that some deposits will be confirmed in our system without confirmations in the blockchain. In this case you will receive only one callback for the transaction. The parameter **"status**" will have the value  **"confirmed".** When we confirm the transaction we are ready to manage all the risks concerning accepting real funds later. You should not be concerned about it.

In other cases you will first receive the callback with the **"not\_confirmed"** status. It will mean that we found the transaction in the mempool but we are not ready to guarantee that it will be received. When this happens you can create the transaction on your side but assign it the status of **"pending"**. After that you should wait for the second callback where the value of **"status"** will be **"confirmed".**
{% endhint %}

{% hint style="warning" %}
#### Attention

You have to validate a signature of the callback and values of known parameters in order to avoid fraudulent activity.
{% endhint %}

In the case of a successful validation of the callback, your system has to respond with **HTTP Code: 200 OK.** No additional parameters are required in the response body. 

Otherwise we will keep the callback in our sending queue and will continue the attempts according to schedule mentioned here: [Callbacks](../api-documentation/callbacks.md).

{% hint style="info" %}
#### Hint 6

You may always go to our backoffice interface and get all the information about the specified callback from the "Transaction info" section, including timings, number of attempts to send the callback, response and so on.

If you had some technical issues with your callback handler or long maintenance period there is a button in the "Transaction info" to reset the callback sending queue. Using this function you can resend the callback immediately.
{% endhint %}

{% hint style="warning" %}
#### Attention

There is a difference between deposit and withdrawal callbacks.

For the deposits, if the user makes all the deposits to the same address, you will receive the same values of **"foreign\_id"** and **"address"** parameters every time. Parameter **"address"** will show which address received funds from the user. It is the address from our system.

For withdrawals, you will receive different values of **"foreign\_id"** and **"address"** parameters in every callback. Parameter **"address"** in this case will show the user's address where we sent funds.
{% endhint %}

{% hint style="info" %}
#### Hint 7

When a user sends you the same amount on the same address you will receive very similar callbacks. In order to understand whether you see several callbacks for the one transaction or if there was more than one transaction, you can use the **"ID"** parameter from the root element in the callback JSON. This parameter is unique for all transactions from our end.
{% endhint %}

{% hint style="info" %}
#### Hint 8

If a user complains that they made a deposit and can't see this deposit on their account we recommend that you do the following steps:

* check the transaction in our backoffice interface.
* if it is confirmed, check the "Transaction info" section to see what your system responded to our callbacks.
* if we can't deliver you the callbacks, check the callback handler on your end.
* if the transaction is not confirmed in our system, go to a blockchain explorer and check if this transaction has a minimum number of confirmations.
* if it doesn't have the defined number of confirmations the user needs to wait until the minimum number of confirmations has been reached.
* if the transaction has the minimum number of confirmations, please contact our support team.

Here you can find the information about the minimum number of confirmations for each cryptocurrency:

* [Confirmations and limits](../confirmations-and-limits.md)
{% endhint %}



