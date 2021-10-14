---
description: Contains withdrawals description and provides common workflow for that feature
---

# Withdrawals

## Withdrawals

To the opposite of deposits, sending cryptocurrencies to the users is similar to classic payment methods. Users fill the form where they provide the address and the amount of the withdrawal. After that the web-service creates the transaction and sends a withdrawal request to the payment provider. When the transaction is confirmed by the payment provider, the web-service decreases the user's balance on the website.

### Common withdrawal workflow

The most common scenario for sending crypto is "withdrawal with exchange". Coinspaid provides web-services with on-the-fly exchange solution. This means that the funds that are stored on a merchant's fiat balance can be automatically converted into cryptocurrencies before being sent to the user's crypto wallet.

In case of regular withdrawals without exchange the workflow will be the same except of conversion operation.

![](<../.gitbook/assets/image (19).png>)

> #### Algorithm
>
> 1. You have EUR balance in our system
> 2. User wants to get a withdrawal from their EUR balance on your site to their BTC wallet
> 3. User uses some kind of “withdrawal” option on your site, chooses BTC as the currency to use for the payout and fills the payout form with their BTC address where they want to receive the funds and the withdrawal amount.
> 4. After that your system makes the request to our processing.
> 5. Our system makes an automatic exchange from EUR to BTC, sends funds to the user’s crypto address and your system gets the callback with transaction parameters, including the transaction's status, currency pairs, amount, fees and so on.
> 6. You decrease the user's EUR balance for the transaction amount

{% hint style="info" %}
#### Hint 

In order to make a withdrawal you should use the **"/v2/withdrawal/crypto"** method from our API.\
You can define what currency should be used to send the funds, and, if necessary, from what fiat currency the funds should be converted before sending to the user.
{% endhint %}

{% hint style="warning" %}
#### Attention

Unlike the "**/v2/addresses/take**" method, you should use the unique "foreign_id" every time you make a withdrawal request to our system. 
{% endhint %}
