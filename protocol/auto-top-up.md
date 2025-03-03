# Auto Top-up

Papaya protocol implements an automatic balance top-up feature. It works as follows: at the moment of liquidation—when your expenses exceed your income—the liquidator first attempts to top up your balance by the amount necessary to cover your subscriptions for one month in advance.&#x20;

<figure><img src="../.gitbook/assets/Refill.png" alt=""><figcaption></figcaption></figure>

This functionality relies on the allowance mechanism of the ERC-20 standard. After that, two scenarios are possible:

&#x20;1\. Auto top-up succeeds. If your balance is successfully replenished with the missing funds for the next month, the liquidator’s transaction fee is deducted from this amount—no extra funds are taken.

&#x20;2\. Auto top-up fails. If topping up your balance is not possible (for instance, due to insufficient allowance or funds), the protocol proceeds with selective liquidation of your subscriptions until equilibrium between incoming and outgoing flow is reached.



> Note: To enable this feature, you must grant the Papaya protocol an allowance of uint256.max(). Even with this maximum allowance, your funds cannot be stolen by the liquidator or anyone else, as the funds are immediately deposited into your own balance, and only you can decide how they are subsequently spent.
