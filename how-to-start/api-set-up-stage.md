# API Set Up Stage

[Previous step is finished](introduction.md)? Are you browsing your merchant account?

![](https://lh3.googleusercontent.com/Rc3ZfEsRSHVpbU\_1W_iIghrQajkeLQFyEOSV8c3B-uWstKFldXfavKKiN32VHl-JXCA5Sa-iaSWjogVEPyrXztcKP2yPfl4zI4swgKMzryP9S1o8EwxxO9f1SL_UoBY9nAE9XLHW)

Great! Now we can go to the next step – setting up the API.

Go over to the API keys menu, where you can activate your API key (or create a new one).

You will receive your **API secret** – an access code for the API key that you’ve activated. You’ll need to copy and save the key secret in a safe place because it is **only displayed once** and you won’t be able to see it again.

![](https://lh3.googleusercontent.com/gZICai8h413pKBVOi8XLvTWYbnz4xOp40NN3RQoyAaQosM1sLVzzB8cJLkUJAH5TDHbjnYFEZmmqupGI-OM82W0C9NScA1Xxk5-qkyl2NTbOrVhAcP-Fq2uQD5FPdJhPTGU1SClb)

{% hint style="danger" %}
**Please note! The API secret is the most important security issue for the production environment. The secret grants access to funds management, hence the person with the secret may transfer funds to any external addresses.**
{% endhint %}

![](https://lh5.googleusercontent.com/rM_yrUMAFNEqiZvDFxL-w8Pl8mkT4t6lBv1qmrNmpXx_YcNllZaC9vqEWi3116ZHj_ApXDcIVonqkClTfqaJ2pLHTuVfGx5lJgQa_hSo-FjZx3stNPI2fjaASwsNDjZPQtJCDcuD)

At this point you may whitelist IP addresses if necessary, to do so you need to press on the pencil button below IPs column.

![](https://lh3.googleusercontent.com/ce9rWH4CS05mCe3E5fPAQR1O23SggdVtnAfYHS_Y9a-lauktJOInaNhKVKhB_hooD6WtuxWxiY1A16EynBPjBjD537gJbz3re-RnVgoybNFT2sEu8NuSjmT011wdyzytbdTHVvcQ)

![](https://lh6.googleusercontent.com/csIry\_4Mv1Jjas4tJThHe9PAhe0CVrWNUFasFlzcVzWWPQ1N8k0URfb0CPZS3CzEkyxKP0J475CHzs5qtNtbJxJb3gsve2cINC8oVwEpUy0EotG4iGGsO_jwwYPMGNh4sjVR6nvE)

{% hint style="warning" %}
Note. This step is optional, you don't need to whitelist specific IP addresses, in case you skip this step all IP addresses will be considered as whitelisted ones and no any restrictions will be applied in this regard.
{% endhint %}

Now you need to set up the address for callbacks from the API. Callbacks are a means of communication with our API. The system sends callbacks for every transaction (deposit or withdrawal) and correct handling of these callbacks is essential for your day-to-day workflow. \
\
You can set up this address by picking the "Settings" tab. 

Then go to the “API” tab located in the top right corner below your balance and set up your URL. You need to complete this step to receive callbacks from us, the system will send them to the URL that you set here.\
Also, you can change the API version here, although** v2 is used by default and we don’t recommend changing it.**

![](https://lh3.googleusercontent.com/rDPpFWTuuY2TsGU-YhZqXm9KlyZazkygyynBvE3IBVxjRFPVX5u-gzBVfSAoqbaMHPQbxLcyQK\_0uyEm\_07xhFE5EH2uoXO7x-zLSLPwxA6BTl9FNJpZxBA1aZKypzdWlxNoBUuH)

Make sure that all necessary currencies are enabled on your merchant account, for that you need to access the “Currencies Info" tab. Here you can enable the currencies that you want to use (either crypto or fiat) by pressing the “Add New Currency” button and picking the desirable currencies from the list

![](https://lh4.googleusercontent.com/AY76aLCXxNdn5vDvZlEWgIBr6p9c1MchiG24wxj0me78yPLVhg9h1CTBpncS4jqxa6YuhFbP0JUzxX8FSRaT9HQXRdXIJwNPTp4BFJ0uLk0FrvpQQRitkK-PUmvNhhHg-N1Yevg3)

