# Confirmations and limits

Here you can find confirmation times for crypto deposits and min/max limits.

{% hint style="danger" %}
Please note that **min limits** for exchange operations must be **obtained via API** \(see [this API call](api-documentation/api-reference.md#get-list-of-exchangeable-currency-pairs)\) because they may vary dynamically. Limits for min deposits and withdrawals can [must be obtained via API](api-documentation/api-reference.md#get-list-of-supported-currencies) too, though they do not change often.
{% endhint %}

| Currency | Confirmations | Min deposit | Min withdrawal | Notes |
| :--- | :--- | :--- | :--- | :--- |
| ADA | 15 | 1 | 1 | [explorer](https://cardanoexplorer.com/) |
| BTC | 0/1 | 0.0002 | 0.0002 | [explorer](https://www.blockchain.com/explorer) |
| BCH | 0/6 | 0.001 | 0.001 | [explorer](https://explorer.bitcoin.com/bch) |
| LTC | 6 | 0.01 | 0.01 | [explorer](https://live.blockcypher.com/ltc/) |
| DOGE | 6 | 1 | 1 | [explorer](https://live.blockcypher.com/doge/) |
| ETH | 10 | 0.01 | 0.01 | [explorer](http://etherscan.io/) |
| XRP | 3 | 0.001 | 0.001 | [explorer](https://xrpcharts.ripple.com/#/) |
| NEO | 10 | 1 | 1 | [explorer](https://neotracker.io/) |
| USDT \(OMNI\) | 2 | 0.0001 | 0.001 | [explorer](https://omniexplorer.info/) |
| USDTE \(ERC20\) | 10 | 0.01 | 0.01 | [explorer](http://etherscan.io/) |
| USDTT \(TRC20\) | 19 | 1 | 1 | [explorer](https://tronscan.org/) |
| ERC20 | 10 | 0.01 | 0.01 | [explorer](http://etherscan.io/) |
| XIN | 9 | 10 | 10 | [explorer](https://explorer.optimusway.io/) |
| BNB | almost instant | 0.01 | 0.01 | [explorer](http://etherscan.io/) |
| BSV | 6 | 0.001 | 0.001 | [explorer](https://blockchair.com/) |
| TRX | 19 | 10 | 10 | [explorer](https://tronscan.org/) |

{% hint style="info" %}
Number of confirmations can be more than value in table in cases when several blocks are released in a short period of time.
{% endhint %}

