---
description: Balances, subscriptions and accrual without a transaction per period.
---

# How it works

This page explains the core mechanics of Papaya. For function signatures, see the [Protocol reference](<../README (1).md>).

## 1. Balance

Each Papaya contract works with one stablecoin on one network, for example USDC on Base.

A user deposits stablecoins into the contract with `deposit`. The contract keeps an internal balance for the user. This balance behaves like a token: it has a name (for example "Streaming USDC"), a symbol (for example "ppUSDC"), and can be queried with `balanceOf`. Internally balances use 18 decimals.

Anyone can fund a user's balance with `depositFor`. This lets a partner, an employer or a merchant pay into a user's balance on their behalf.

Users withdraw with `withdraw` or `withdrawTo`. A balance can also be sent to another Papaya account directly with `pay`, without leaving the contract.

## 2. Subscriptions

A subscription connects a payer and a recipient (the "author") inside a project:

* **Payer:** the user who pays.
* **Author:** the merchant, creator or service that receives the payment.
* **Project:** the platform the subscription belongs to. Each project has an ID and an admin.

When a user subscribes, the contract records how much they pay and to whom. Incoming and outgoing amounts are aggregated per account.

## 3. Accrual without transactions

Papaya does not run a job that processes every subscription each period. There is no batch transaction and no keeper that charges users one by one.

Instead, every account stores:

* its balance at the last update,
* its total incoming rate,
* its total outgoing rate,
* the time of the last update.

The current balance is calculated from these values whenever it is needed: last balance plus (incoming minus outgoing) multiplied by time passed. This works the same for an account with one subscription or a hundred, and the contract never loops over subscriptions to do it.

That is why the cost of a subscription does not grow with the number of periods. Between user actions, accrual costs nothing.

## 4. Project fees

Each project can take a fee from subscriptions made inside it:

* The project admin sets a default fee for the project, and can set a different fee for specific authors.
* The fee is a share of each subscription, up to 20%.
* The fee flows to the project owner the same way the rest of the payment flows to the author.

## 5. Merchant withdrawals

Authors and project owners see their balance grow as subscriptions accrue. They can withdraw it at any time in one transaction, no matter how many subscribers they have.

## 6. Keeping subscriptions funded

A subscription only runs while the payer's balance can cover it. Papaya has two mechanisms for this: **refill** from the user's wallet and **liquidation** when refill is not possible. See [Balance, refill and liquidation](balance-refill-and-liquidation.md).

## Summary

| Action                               | Who sends the transaction               |
| ------------------------------------ | --------------------------------------- |
| Deposit, subscribe, cancel, withdraw | The user (or a relayer on their behalf) |
| Monthly or per-second accrual        | Nobody, it is calculated                |
| Merchant collects revenue            | The merchant, once, whenever they want  |
| Refill or liquidation                | Anyone, rewarded by the protocol        |
