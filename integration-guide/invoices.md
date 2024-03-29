---
description: >-
  This feature provides an opportunity to create an invoice for a B2B or B2C
  client for a specified amount.
---

# Invoices

## Invoice general flow

You should send a request with a particular set of fields to create an invoice.The response will contain an URL that you have to forward to the user for payment.

Your user will see an invoice name, amount and currency, and also specific parameters (depending on invoice type): timer, possibility to choose payment currency or estimated amount and currency of payment.

If you send user's email in request, this field will be filled out for the user. Otherwise, the user has to fill out this field themselves. After confirming currency and putting email, the user has to pay an invoice using a specified address before the expiry of the timer. This address is generated by CoinsPaid.

The invoice type will be externalized depending on the sent parameters. There are 3 types of invoice:

1. Invoice without restriction of payment time. The user chooses a currency of payment themselves without time restriction. Rate will be fixed when the user confirms payment currency.
2. Invoice with time restriction. The user chooses a currency of payment themselves, but the time restriction will be 15 minutes starting from invoice creation.
3. Invoice with time restriction and without a possibility to choose payment currency. The user sees the amount and payment currency that they need to pay.

If the user fails to pay the invoice in due time the system will display failed status.

You will receive a callback about the successful transaction creation after it appears in the mempool. We will change the timer from 15 minutes to 24 hours. During this period of time the transaction will change its status to confirmed.

After the successful confirmation of the transaction, funds will be exchanged in a receiver currency and transferred to your account. The Merchant is charged a Fee for Operation after the Funds are credited to the account.\
\
If the invoice payment can paid by installments, you will receive a callback for each part.

If the user sends an amount of funds that is more or less than specified one we will send a payback guideline to their email.\
\
[Here](../api-documentation/api-reference.md#create-invoice) you can find the API Endpoint for invoices.

## Invoice statuses

![](<../.gitbook/assets/Witdrawal Flow.png>)

## Invoice Type

### **1st Type**&#x20;

#### Invoice without restriction of payment time

This invoice type allows the user to choose the payment currency themselves without a time restriction. The rate will be fixed when the user confirms the payment currency.

By following the link the user will see the information about the invoice and also will be able to choose the payment currency.

![](<../.gitbook/assets/image (21).png>)

After confirming the currency and putting email, the rate will be fixed for 15 minutes. During this period of time the user has to pay the invoice using the specified address.

![](<../.gitbook/assets/image (22).png>)

### **2nd Type**

#### Invoice with time restriction&#x20;

This invoice type allows the user to choose the payment currency themselves, but the time restriction will be 15 minutes starting from the invoice creation.

By following the link the user will see the information about the invoice, timer and will also be able to choose the payment currency. The rate will be fixed after the invoice creation.

![](<../.gitbook/assets/image (25).png>)

After confirming the currency and inputting the email, the user has to pay the invoice using the specified address before the expiry of the timer.

![](<../.gitbook/assets/image (26).png>)

### **3rd Type**&#x20;

#### Invoice with time restriction and without the possibility to choose payment currency

This invoice type allows the user to pay the invoice themselves in a definite currency with a time restriction for 15 minutes starting from invoice creation.

By following the link the user will see the information about the invoice, 15 minutes timer and the payment currency. The rate will be fixed after the invoice creation.

The user has to pay the invoice using the specified address before the expiry of the timer.

![](<../.gitbook/assets/image (28).png>)

[Here](../api-documentation/callbacks.md#invoice-types-callbacks) you can see an example of a callback for each type of invoice.

## Invoice failed

Invoice fails upon the occurrence of any of the following:

1. 15 minutes timer expiration.
2. Transaction has processing status for more than 24 hours.
3. The user paid an amount less than was requested. In this case the transaction will have a confirmed status but invoice will have a failed status.

[Here](../api-documentation/callbacks.md#invoice-payment-callbacks) you can see successful and unsuccessful examples of invoice payment callbacks.&#x20;
