# Payment Terminal

Payment Terminal is a separate service which can help you to display your deposit address as a web page or embed it into your website as an i-frame.

As a merchant you need to generate a GET URL with a set of the established parameters according to the requirements below and redirect a user via that link to Payment Terminal. Data available for the user includes address and QR-code, currency and deposit amount (in case ‘amount’ parameter was sent).

![An example of implementation of Payment Terminal with i-frame](<../.gitbook/assets/image (29).png>)

![An example of implementation of Payment Terminal without i-frame](<../.gitbook/assets/image (30).png>)

Once the user makes a deposit, it will be processed according to common deposit flow.

### Payment terminal workflow representation

![](<../.gitbook/assets/image (32).png>)

## Creating a request

You need to create a request which contains hash with two required parameters: data and signature.

The request address:

**https://terminal.coinspaid.com/?'data and signature'**

### **Data parameter generation**

You need to form JSON with [the following parameters](../api-documentation/api-reference.md#payment-terminal-json-parameters)

**Example:**

```php
{	
  "client_id"=>11,
  "currency"=>"BTC",
  "foreign_id" =>111,
}
```

You need to convert the resulting represented code in JSON to base64 format.

**Example:**

```
eyJjbGllbnRfaWQiOjExLCJjdXJyZW5jeSI6IkJUQyIsImZvcmVpZ25faWQiOjExMX0
```

You need to:

* concatenate JSON with secret key to generate signature

**Example:**

```php
{	
  "client_id"=>11,
  "currency"=>"BTC",
  "foreign_id" =>111,
}
  ObPvxgtazKCkQ7ifz3qzocbv9TVXeB1LUIbCsYk2WUt5agvyt1n1MhQnnCBlcwhY
```

* The calculated hmac(sha512) hash in lowercase looks like:

**Example:**

```
fbd85d7769b05ee170486e1b294047707ad1c7cb55c3be2b1516339e8cdf900d76657074d7105797f0361d28b768ad01b62d44a48b52b8d2581bf5e63f72ca3a
```

As a result, the request will have the following look:

```
https://terminal.coinspaid.com/?data=eyJjbGllbnRfaWQiOjExLCJjdXJyZW5jeSI6IkJUQyIsImZvcmVpZ25faWQiOjExMX0=&signature=fbd85d7769b05ee170486e1b294047707ad1c7cb55c3be2b1516339e8cdf900d76657074d7105797f0361d28b768ad01b62d44a48b52b8d2581bf5e63f72ca3a
```
