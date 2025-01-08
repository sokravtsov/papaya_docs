# Overview

Papaya is a scalable subscriptions protocol that enables per-second payments. Unlike competitors, Papaya does not use token proxies but works with native assets, allowing you to retrieve your funds back to your wallet at any time.

* Each Papaya contract is designed to operate with a single specific token. At present, we exclusively support stablecoins: USDT, USDC, and DAI.
* Each Papaya contract functions independently, operates solely with its predetermined token, and remains unaffected by subscriptions involving other tokens.
* Our contracts provide robust support for the creation, modification, and deletion of subscriptions, ensuring flexibility and control.
* Every subscription is uniquely tied to a specific wallet, guaranteeing that users are accountable only for their expenses and can rely on the security of their funds.
* Our contract architecture supports the collection of payments from an unlimited number of subscribers within a single transaction.
* Distinguishing ourselves from competitors, Papaya adheres strictly to widely accepted ERC20 standards, ensuring compliance with the highest security requirements.

## Computational complexities

***

* `n` - number of subscribers
* `m` - number of products and authors

| Action   | TON Subs   | Papaya Subs |
| -------- | ---------- | ----------- |
| Deposit  | `-`        | `O(n)`      |
| Withdraw | `-`        | `O(n)`      |
| Claim    | `O(n * m)` | `O(m)`      |

## Example

***

Imagine `10,000` products and authors having `1,000,000` of subscribers each. This would lead to `10,000,000,000` of txs per month/week.
