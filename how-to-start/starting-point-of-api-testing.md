# Starting Point of API Testing

Now, which first steps should you take to test our system?

At this point you should have familiarized yourself with [the previous sections](../api-documentation/api-reference.md) of our API documentation.

A good place to start is to generate new addresses. You can do this by using this request request -&#x20;

```
https://app.cryptoprocessing.com/api/v2/addresses/take
```

In order to test the depositing function, you can send some currency to these addresses. You can transfer some test currency from any testnet faucet, for example - a BTC [testnet faucet](https://coinfaucet.eu/en/btc-testnet/). Once the test funds are obtained you can send a part of it back to an address specified on the faucet's page using [API request](../api-documentation/api-reference.md#withdraw-cryptocurrency) in order to test a withdrawal flow to an external address.

Please note, you will be able to test the exchange function with testnet currency only in our Sandbox environment, you won’t be able to do that with your account in the production environment. Please make sure to test the feature at this stage. You will still be able to use the exchange feature in the production environment, but only with real funds.

{% hint style="danger" %}
Since you are not in our production environment, for your request you should use sandbox.coinspaid.com as well. For example, instead of **https://app.cryptoprocessing.com**/api/v2/addresses/take you should use the following format – **https://app.sandbox.cryptoprocessing.com**/api/v2/addresses/take**.**
{% endhint %}

By this time, if you followed the steps above and already set your callback URL, you should start receiving them from our system. Make sure that the callbacks are processed correctly on your end and you receive them for all ongoing transactions. In case you haven’t received the callback when you should have, you can press “Repeat callback” and our API will send it to you again. If the issue persists or you have any further questions about API, don’t hesitate to contact us via [support@cryptoprocessing.com](mailto:support@cryptoprocessing.com).

![](<../.gitbook/assets/Снимок экрана 2021-05-04 в 18.45.28 (1).png>)

[This documentation section](./) was aimed to cover the basics and help you to understand how our API functions.\
We hope that the information was helpful to you and we are looking forward to building a strong business relationship in the future!
