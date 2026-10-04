---
description: What happens when a balance runs low.
---

# Balance, refill and liquidation

A subscription runs only while the payer's balance can cover it. This page explains what happens when the balance runs low.

## Ways to keep a balance funded

1. **Deposit in advance.** The user deposits enough for many periods.
2. **Partner funding.** A partner, employer or merchant funds the user's balance with `depositFor`. This is the simplest option for fintechs and wallets: the user never has to top up manually.
3. **Automatic refill.** The user gives the Papaya contract an allowance on their wallet. When the balance gets low, the contract pulls a refill from the wallet.

## Refill and liquidation

Both happen through one function, `liquidate(account)`, which anyone can call once an account qualifies.

**When an account qualifies**

* **Streaming:** when the balance will not cover the next day of outgoing payments plus the cost of a liquidation.
* **Periodic:** during the last day before a new period, if the balance will not cover the next period.

**What happens**

When `liquidate` is called, the contract first tries to refill:

* **If the user's wallet has an allowance and enough funds**, the contract pulls a refill and the subscriptions keep running.
  * Streaming: the refill covers about 30 days of net outgoing payments.
  * Periodic: the refill covers one period.
  * The caller receives a small reward from the refill to cover their gas. In streaming, the reward is based on the current network gas price. In periodic, it is a small fixed amount.
* **If refill is not possible** (no allowance or not enough funds in the wallet), the account is liquidated:
  * all of the user's subscriptions are cancelled,
  * Streaming: the caller receives the remaining balance as a reward,
  * Periodic: the caller receives a small fixed reward per subscription, and the rest of the balance stays with the user.

**Why anyone can call it**

Refill and liquidation are open to everyone and rewarded by the protocol, so they do not depend on Papaya running a server. Partners and Papaya can also run their own keepers. On networks with expensive gas, such as Ethereum mainnet, external callers may not find the reward worth it, so a partner or Papaya keeper is recommended.

## Safety checks

The contract blocks actions that would put a streaming account at immediate risk:

* `subscribe` reverts with `TopUpBalance` if the balance would not cover about two days of payments.
* `withdraw` and `pay` revert with `ReduceTheAmount` if they would leave less than about two days of payments.

## What Papaya does not do

* There is no grace period and no automatic retry after a failed refill.
* There is no dunning (reminder emails, retry schedules). If a merchant needs this, it is handled off-chain by the merchant or a partner.
