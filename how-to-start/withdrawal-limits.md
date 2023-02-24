# Withdrawal Limits

In order to control and secure your funds, we have added the ability to configure withdrawal limits, which can be created both via the API and the interface.

With this functionality, you can set up a default limit and specify a custom limit for a specific currency.

Withdrawals that exceed the limit will obtain the Pending status. All users whose email addresses are specified in the settings will receive email notifications with a link to the transactions list with Pending status. You can approve or decline transactions with the Pending status.

Setting limits on withdrawals and confirmation of withdrawals exceeding the limit are available only to users with "Owner" permissions within the merchant account.

{% hint style="danger" %}
Please note that transactions **cannot** be created and confirmed **by the same owner**. If you only have one owner account, then the “Interface withdrawals” functionality is not available to you.
{% endhint %}

To set up withdrawal limits, you need to go to the Settings → Withdrawal limit. In this tab, select which withdrawals you are going to limit: created via API or the interface.

![](https://lh4.googleusercontent.com/WfiB3CA2cVlXE7qguA0srD0LLYhHJQfy3931OM29wkhnICp6f7W2tjeV0miynmRPpT48F4k-n7eZWl62VS9C4WxQ7mhXrGx4uVqBqqDYzTMek50xGVM1iVHphQOEoAEN87XWTTr3)

There are three types of limits that you can set:

* Limit for one operation;
* Limit on transactions per hour;
* Limit on transactions per day.

If no limits are defined, the value is set at Unlimited.

## **Default interface withdrawal limits**

You can set up the default limit for all withdrawals via the interface. All default limits are set in equivalent to the EUR.

![](https://lh5.googleusercontent.com/4lPLbXzehl3P8UxVH4os7L4bONvMpw9PHso-cOnPP4L5-607YhsqdJ8i4GI5Bvb1B7\_XgYYAW1evr-pxy3ELXIHur0awePZ8H\_g30uHFWrn\_p\_4oR8GG884diEcxt8vhsgj2iaCO)

This setting will be applied to all withdrawals via the interface/API for all cryptocurrencies.

To set it up, click on the “Edit” button.

![](https://lh5.googleusercontent.com/gNoMgoCPfLYIp8IvaWpPioSPgpkg49KlkSLX5FhCfJjQqI2ar7z5UeR7J04aenGCMRAs3tB5xzWiGkEgVpuzCuwEjkP8PSEc97pm95cHKpXna\_CqvfXM2sux44nvTbJ8Lpul24lR)

In this form, you can do the following:

* select the option “All interface withdrawals will be passed through manual moderation”(all interface withdrawals are manually moderated);
* for each type of operation (one operation, per hour, per day):
  * leave Unlimited **** value (all interface withdrawals for the type of operation are unlimited);
  * select Custom and add a value (all interface withdrawals for the type of operation with a value higher than this one are manually moderated).

After setting the limit, enter your 2FA code to confirm.

## **Custom withdrawal limits**

To set a limit for any specific currency, go to the “Custom interface/API withdrawal limits” section.&#x20;

![](https://lh6.googleusercontent.com/0bynfrV2-vFx-eCepfMTDCceAi\_wgrwL4jwFXbwjHXW7jo6-0INZKQRQa0smZrEAbpylryzPJPC1uXNCavgoyutrs3OYBjEUs2F6rG3lv-zgY\_\_aiYetfjc5AIU6iFkRdbmaqehf)

To add a limit on withdrawals for the cryptocurrency, click “Add limit.”

![](https://lh5.googleusercontent.com/UQ9FI94nZhb7mIQDHL083en4eEGa-uMBS1\_Zd7w3lPhZRHr\_qypNvgMb7FKLYOezmowrJQEbMD1xecmLFA\_kGLqgbYbpi51C\_71MXAVJvjKrAWu43G4eCK9xdCJPix0OFQLQZZBq)

In the window that appears, select the currency from the drop-down list. The next steps are similar to the Default settings.

When specifying your amount, you cannot set the value **** to "0" since it will be considered that you want to send all transactions for manual moderation. In case you want a similar setting, check the box “All interface/API withdrawals will be passed through manual moderation.”

{% hint style="danger" %}
**Custom withdrawal limits have higher priority than the Default withdrawal limits. For example: 1 BTC = 10,000 EUR. The user sets a “per day” default withdrawal limit to 9000 EUR and a single operation custom withdrawal limit in BTC to 2 BTC. When you withdraw 1 BTC, the transaction will NOT obtain the “Pending” because it will be less than the set custom withdrawal limit.**
{% endhint %}

\
\
\
\
\
\
