---
description: Contains exchanges description and provides closer look at its features
---

# Exchanges

## Exchanges

While on-the-fly deposits and withdrawals are possible and mostly oriented towards end users, there is a way perform conversion of funds (either crypto to fiat, fiat to crypto or crypto-crypto) with existing merchant balances as long as the exchange pair [is supported](../) by the processing. The exchange feature is available via [API](../api-documentation/api-reference.md#calculate-exchange-rates) as well as backoffice, the latter option suits Business Wallet integration type the most in case on-the-fly exchange wasn't used initially. 

{% hint style="info" %}
**There are 3 API methods that are associated with exchanges:**\
****\
**** [v2/exchange/calculate](../api-documentation/api-reference.md#calculate-exchange-rates) - a request that doesn't perform an exchange by itself, but allows to obtain an actual ratio for the subsequent exchange. It can be used both as for obtaining general information about the actual rates for a crypto exchange as well as receiving and fixating exchange ratio for[ fixed exchange API method](../api-documentation/api-reference.md#exchange-on-fixed-exchange-rate). The obtained ratio is viable for one minute, after that another request for an actual ratio calculation should be sent;\
[v2/exchange/fixed ](../api-documentation/api-reference.md#exchange-on-fixed-exchange-rate)- allows to perform an exchange with fixed ratio obtained from the request above. **Note -** the required parameter "_price_" can be obtained from the method above.\
[v2/exchange/now](../api-documentation/api-reference.md#exchange-regardless-the-exchange-rate) - allows to perform an exchange without specifying the ratio beforehand, this method uses an actual ratio from a trading platform at the moment of sending this request to our API.
{% endhint %}

{% hint style="warning" %}
**Note**\
****\
****The exchange feature via the backoffice is implemented via the [v2/exchange/fixed](../api-documentation/api-reference.md#exchange-on-fixed-exchange-rate) method, the exchange ratio changes every minute and is automatically displayed within the respective tab.
{% endhint %}

{% hint style="danger" %}
The minimum exchange amount is equivalent to 0.003 BTC (This limit does not relate to the on-the-fly deposits and withdrawals. In order to get the actual information about the on-the-fly transactions please refer to the [Confirmations and limits](../confirmations-and-limits.md) section).

More detailed information about **min limits** of exchange operations for particular currencies must be **obtained via API** (see [this API call](../api-documentation/api-reference.md#get-list-of-exchangeable-currency-pairs)) because they may vary dynamically.
{% endhint %}
