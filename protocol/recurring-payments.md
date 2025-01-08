# Recurring Payments

<figure><img src="../.gitbook/assets/Картинка от одного к другому.png" alt=""><figcaption></figcaption></figure>

In traditional systems, subscription payments are automated and seamless. However, in blockchain environments, smart contracts require explicit calls to operate, posing challenges for background operations. Consequently, processing subscription payments necessitates individual calls to deduct the agreed-upon amount from each subscriber.

To address this, Papaya employs a time series mechanism. By tracking spending and earning rates per second, we can calculate user balances in real-time. Papaya represents each user through incoming and outgoing streams.

To determine the per-second token transfer rate, use the formula: Desired Value / Time (seconds). For example, to receive 30 USDT monthly, calculate as follows:

```mathematica
30 USDT * 1e12 / (86400 * 30.5) = 11,384,335,154,826.
```

{% hint style="info" %}
Note: Economists consider each month as 30.5 days to mitigate the impact of leap years.
{% endhint %}

{% hint style="warning" %}
Despite USDT having 8 decimals, we standardize all tokens to 1e18. Therefore, upon deposit, tokens are multiplied by the appropriate factor to align with this standard.
{% endhint %}
