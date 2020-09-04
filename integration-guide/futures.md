---
description: >-
  The rates of the cryptocurrencies may change few times in a second. In order
  to provide the best experience of using our API we implemented a new solution
  for fixating the cryptocurrency rates.
---

# Futures

Usage of this function makes possible to fixate cryptocurrency exchange rate for short period of time. It allows you to receive an established amount of the currency to your fiat balance regardless of the exchange rates fluctuations.

Let’s say you want to implement a new button “Deposit 100 EUR now” from your side. Considering that cryptocurrency rates changing every second, you will not be able to request the correct cryptocurrency amount from the user. To resolve this issue you can use the new function - “Futures“.

In this case we fixate the cryptocurrency rates for a short period time and set the exact amount in cryptocurrency to the user. The implementation of this function has two steps:

1.  [Requesting info concerning the rates for the futures](https://docs.coinspaid.com/docs/api-documentation/v2#calculate-rates-for-futures): You get the current exchange rates for the specified address according to the currency pairs linked to this address and different available amount ranges. These rates will be fixated for 10 minutes from "ts\_fixed" to "ts\_release" \(timestamp format\) time period.
2.  [Requesting info concerning a confirmation of the futures transaction](https://docs.coinspaid.com/docs/api-documentation/v2#confirm-futures-transaction): At this step you define the amount in a fiat currency that you want to accept from the user and get the exact amount of the cryptocurrency that the user needs to send within the mentioned time period from "ts\_fixed" to "ts\_release" \(timestamp format\).

If the user deposits mentioned amount within set time period you will receive exactly 100 EUR. If the user fails to do so, the exchange process uses currently actual cryptocurrency rates.

The process from your side should take the following form:

* A user presses the button “Deposit 100 EUR now”. In this case your system sends the request \([calculate-rates-for-futures](https://docs.coinspaid.com/docs/api-documentation/v2#calculate-rates-for-futures)\) for the specific address.
* After that you receive the [callback](../api-documentation/callbacks.md#futures-callback).
* You can use this callback to check the rates of the deposited amount. The cryptocurrency rates will be fixated at this step.
* If the user agrees with these rates and presses “Agree” your system sends the following request \([confirm-futures-transaction](https://docs.coinspaid.com/docs/api-documentation/v2#confirm-futures-transaction)\).
* And receives[ the callback](../api-documentation/callbacks.md#futures-callback).

Upon the completion of that step our system would be able to process the transaction, and the user obtains your deposit address and time period during which the deposit must be completed. This is achieved by receiving the parameter “sender\_amount” which contains the amount in the cryptocurrency that the user needs to deposit in order to receive 100 EUR. The deposit address should be provided to the user at this stage as well.

As soon as the user deposits the mentioned amount within the established time period, exactly 100 EUR should be credited to that user’s balance. If the user sends a different amount in BTC, another amount in EUR will be received as well. If the user deposits outside of the established time frame, the actual ratio in EUR will be calculated via current exchange rates from crypto trading platforms i.e. Kraken or Binance \(previously calculated rates for the futures won’t be taken into account in this case\).

