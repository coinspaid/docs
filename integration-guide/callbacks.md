---
description: Description of API notifications
---

# Callbacks

Asynchronous payments are very popular with cryptocurrencies. In such deposit flow you have to generate an address and pass it to your client. This will be his deposit address which he will be reusing during his lifetime with you. In such payment flow we will notify you about any incoming payments with callbacks.

Owner of the merchant can set up callback URL manually in merchant's settings, and upon processing payments, CoinsPaid will send you notifications in JSON format with all required information about transaction such as amount and status.

Callback retry schedule:\
\
1, 5, 10, 15, 20, 30, 60, 90, 120, 150, 180, 210, 240 minutes.\
\
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

In the case of a successful validation of the callback, your system has to respond with **HTTP Code: 200 OK.** No additional parameters are required in the response body.&#x20;

Otherwise we will keep the callback in our sending queue and will continue the attempts according to schedule mentioned above.

{% hint style="info" %}
#### Hint 1

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
#### Hint 2

When a user sends you the same amount on the same address you will receive very similar callbacks. In order to understand whether you see several callbacks for the one transaction or if there was more than one transaction, you can use the **"ID"** parameter from the root element in the callback JSON. This parameter is unique for all transactions from our end.
{% endhint %}

{% hint style="info" %}
#### Hint 3

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

[Here](../api-documentation/callbacks.md#deposit-callbacks) you can find the examples of the specific callback for each type of operation.
