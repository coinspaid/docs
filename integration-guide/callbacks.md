---
description: Description of API notifications
---

# Callbacks

Asynchronous payments are very popular with cryptocurrencies. In a typical deposit workflow, you have to generate an address and pass it to your client. This will be their deposit address, which they will reuse for a lifetime with you. In such a deposit workflow, we will notify you of any incoming payments with callbacks.

If you have been assigned the “Owner” role for your CoinsPaid merchant account (see [User Permissions](../how-to-start/user-permissions.md)), then you can configure the callback URL manually in the merchant's settings. Upon processing the payments, CoinsPaid will send you notifications in JSON format to this URL with all necessary information about the transaction, such as its amount and status.\
\
Our callbacks contain all the important information about the transaction:

* status
* currency
* amount
* blockchain transaction's hash
* address
* fees
* number of confirmations

and so on.

### A note about deposit callback statuses

For [Deposits](deposits.md), our system supports instant confirmations. This means that some deposits will be confirmed in our system without confirmation in the blockchain. In such a case, AlphaPo will immediately send you a callback with the `confirmed` status. Confirming the transaction, we are ready to manage all the risks associated with accepting real funds later. You should not be concerned about this.

In other cases, you will first receive a callback with the `not_confirmed` status. This will mean that we have found a transaction in the mempool but we are not ready to guarantee that it will be completed. When this happens, you can create a transaction on your side, but assign it the `pending` status. After that, you should wait for the second callback, where the value of the `status` parameter will be `confirmed`.

### Validating callbacks

To provide authentication for the callback, CoinsPaid signs the POST request with your API key and secret key:

* `X-Processing-Key` — Your public key
* `X-Processing-Signature` — The POST request body signed by your secret key using the HMAC-SHA512 hash function

You must validate the signature of the callback and the values of known parameters to avoid fraud.

If the callback is validated successfully, your system should respond with the 200 OK HTTP code. No additional parameters are required in the response body.

Otherwise, we will keep the callback in our sending queue and continue the attempts according to the following schedule: 1, 5, 10, 15, 20, 30, 60, 90, 120, 150, 180, 210, 240 minutes.

### Callbacks in the back-office

You can always go to our back-office interface and get all the information about any specific callback in the **Transaction info** section, including timings, the number of attempts to send the callback, the format of the response, and so on.

If you have technical issues with your callback handler or a long maintenance period, there is a button in the **Transaction info** section to reset the callback sending queue. Using this function, you can resend the callback immediately.

### Foreign IDs and distinguishing callbacks

There is a difference between callbacks for deposits and withdrawals.

In the case of deposits, if a user makes all deposits to the same address, you will receive the same values of the `foreign_id` and `address` parameters each time. The `address` parameter will show you which address received funds from the user. This is the address from our system.

In the case of withdrawals, you will receive different values of the `foreign_id` and `address` parameters in each callback. In this case, the `address` parameter will show you the user's address to which we sent funds.

{% hint style="info" %}
When a user sends you the same amount to the same address, you will receive very similar callbacks. To understand whether you see several callbacks for the same transaction, or there was more than one transaction, you can use the `id` parameter from the root element in the callback JSON. This parameter is unique for all transactions from our side.
{% endhint %}
