# Payment Terminal

Payment Terminal is a separate service which can help you to display your deposit address as a web page or embed it into your website as an i-frame.

As a merchant you need to generate a GET URL with a set of the established parameters according to the requirements below and redirect a user via that link to Payment Terminal. Data available for the user includes address and QR-code, currency and deposit amount \(in case ‘amount’ parameter was sent\).

![An example of implementation of Payment Terminal with i-frame](../.gitbook/assets/image%20%2847%29.png)

![An example of implementation of Payment Terminal without i-frame](../.gitbook/assets/image%20%2846%29.png)

Once the user makes a deposit, it will be processed according to common deposit flow.

### Payment terminal workflow representation

![](../.gitbook/assets/image%20%2843%29.png)

## Creating a request

You need to create a request which contains hash with two required parameters: data and signature.

The request address:

**https://terminal.coinspaid.com/?'data and signature'**

### **Data parameter generation**

You need to form JSON with [the following parameters](../api-documentation/api-reference.md#payment-terminal-json-parameters)

**Example:**

```php
{
  "client_id":1 ,
  "url_back":"https:\/\/coinspaid.com\/?1588146480",
  "amount":0.0005,
  "foreign_id":"15881464801588146480",
  "currency":"BTC",
  "convert_to":"EUR"
}
```

You need to convert the resulting represented code in JSON to base64 format.

**Example:**

```text
eyJhZGRpdGlvbmFsX3BhcmFtZXRlcnMiOnsiY2xpZW50X2lkIjoxfSwidXJsX2JhY2siOiJodHRwczpcL1wvY29pbnNwYWlkLmNvbVwvPzE1ODgxNDY0ODAiLCJhbW91bnQiOjAuMDAwNSwiZm9yZWlnbl9pZCI6IjE1ODgxNDY0ODAxNTg4MTQ2NDgwIiwiY3VycmVuY3kiOiJCVEMiLCJjb252ZXJ0X3RvIjoiRVVSIn0=
```

### **Signature parameter generation**

You need to:

* concatenate JSON with secret key to generate signature

**Example:**

```php
{
  "pay_method":"method_x",
  "user":"user1",
  "amount":32.44,
  "currency":"USD"
  }
  ObPvxgtazKCkQ7ifz3qzocbv9TVXeB1LUIbCsYk2WUt5agvyt1n1MhQnnCBlcwhY
```

* The calculated hmac\(sha512\) hash in lowercase looks like:

**Example:**

```text
9e4c091dbcc9e2eca21e2e3bd6300ebec225dd0d80f4c309da9ace88000bf6da804262c1415a0b956d1d9411e05f55a547b234ce86338bc55ba58c9962ca0dad
```

As a result, the request will have the following look:

```text
GET https://terminal.coinspaid.com/?data=eyJjbGllbnRfaWQiOjEsImN1cnJlbmN5IjoiQlRDIiwiZm9yZWlnbl9pZCI6MTU4OTI2ODI1N30=&signature=9e4c091dbcc9e2eca21e2e3bd6300ebec225dd0d80f4c309da9ace88000bf6da804262c1415a0b956d1d9411e05f55a547b234ce86338bc55ba58c9962ca0dad
```

