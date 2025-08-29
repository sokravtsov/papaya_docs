---
description: Interaction with the contract is facilitated through our SDK.
---

# Interaction

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

For user convenience, Papaya supports integration with all existing wallets through the use of standard ERC20 methods: _balanceOf_, _name_, _symbol_, and _decimals_. When funds are deposited into the contract, an abstract token _pp\*_ (where _\*_ is the original token's name) will appear in the user's wallet.

{% hint style="info" %}
By abstract, we mean that no new tokens are created; instead, we mimic the token. This allows you to add Papaya as a token to your wallet and track your balance seamlessly.
{% endhint %}

{% content-ref url="protocol/core-functions/subscription-management.md" %}
[subscription-management.md](protocol/core-functions/subscription-management.md)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}
