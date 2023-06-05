# Confirmations and limits

Here you can find confirmation times for crypto deposits and min/max limits.

{% hint style="danger" %}
Please note that **min limits** for exchange operations must be **obtained via API** (see [this API call](api-documentation/api-reference.md#get-list-of-exchangeable-currency-pairs)) because they may vary dynamically. Limits for min deposits [can be obtained via API](api-documentation/api-reference.md#get-list-of-supported-currencies) too, though they do not change often.
{% endhint %}

| Currency      | Confirmations  | Min deposit | Min withdrawal | Notes                                                                             |
| ------------- | -------------- | ----------- | -------------- | --------------------------------------------------------------------------------- |
| ADA           | 15             | 1           | 1              | [explorer](https://cardanoexplorer.com/)                                          |
| BTC           | 0/1            | 0.0001      | 0.0002         | [explorer](https://www.blockchain.com/explorer)                                   |
| BCH           | 0/6            | 0.001       | 0.001          | [explorer](https://explorer.bitcoin.com/bch)                                      |
| LTC           | 6              | 0.01        | 0.01           | [explorer](https://live.blockcypher.com/ltc/)                                     |
| DOGE          | 6              | 1           | 1              | [explorer](https://live.blockcypher.com/doge/)                                    |
| ETH           | 10             | 0.01        | 0.01           | [explorer](http://etherscan.io/)                                                  |
| XRP           | 3              | 0.001       | 0.001          | [explorer](https://xrpscan.com/)                                                  |
| CSC           | 1              | 1           | 1000           | [explorer](https://xrpscan.com/)                                                  |
| USDTE (ERC20) | 10             | 5           | 5              | [explorer](http://etherscan.io/)                                                  |
| USDTT (TRC20) | 19             | 2           | 1              | [explorer](https://tronscan.org/)                                                 |
| USDC          | 10             | 5           | 5              | [explorer](https://etherscan.io/token/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48) |
| ERC20         | 10             | 0.01        | 0.01           | [explorer](http://etherscan.io/)                                                  |
| BNB           | almost instant | 0.01        | 0.01           | [explorer](https://explorer.binance.org/)                                         |
| BNB-BSC       | 25             | 0.01        | 0.01           | [explorer](https://bscscan.com/)                                                  |
| BUSD          | 25             | 5           | 5              | [explorer](https://bscscan.com/)                                                  |
| SNACK         | 25             | 10          | 10             | [explorer](https://bscscan.com/)                                                  |
| TRX           | 19             | 10          | 10             | [explorer](https://tronscan.org/)                                                 |
| DAI           | 10             | 5           | 5              |                                                                                   |
| VERSE         | 10             | 10000       | 10000          | [explorer](https://etherscan.io/token/0x249cA82617eC3DfB2589c4c17ab7EC9765350a18) |

{% hint style="info" %}
The number of confirmations can be more than the value in the table in cases when several blocks are released in a short period of time.
{% endhint %}
