# Auto Refill

In addition to the liquidation process, our protocol implements an automatic balance top-up feature. It works as follows: at the time of liquidation—when your spending exceeds your incoming funds—the liquidator first attempts to refill your balance by the difference (delta) between your incoming and outgoing flow. This functionality relies on ERC-20 allowance mechanics. From there, two scenarios are possible:

&#x20;1\. Auto refill succeeds. If your balance is successfully replenished with the missing funds for the next month, the liquidator’s transaction fee is deducted from this amount—no extra funds are taken.

&#x20;2\. Auto refill fails. If topping up your balance is not possible (for instance, due to insufficient allowance or funds), the protocol proceeds with selective liquidation of your subscriptions until equilibrium between incoming and outgoing flow is reached.

\


Note: To enable this feature, you must grant the Papaya protocol an allowance of uint256.max(). Even with this maximum allowance, your funds cannot be stolen by the liquidator or anyone else, as the funds are immediately deposited into your own balance, and only you can decide how they are subsequently spent.
