---
description: Streaming per second or a fixed amount per period.
---

# Subscription modes

Papaya offers two modes. They share the same balance model and the same principle: no transaction per period. They are deployed as separate contracts.

## Streaming

In streaming mode a subscription has a **rate**: an amount per second. Value moves from payer to author continuously.

**How it works**

* The user subscribes with `subscribe(author, subscriptionRate, projectId)`, where `subscriptionRate` is the amount per second.
* From that moment the payer's balance decreases and the author's balance increases every second.
* The user cancels with `unsubscribe(author)`. The stream stops immediately. Nothing is charged after that.

**Requirements**

* To subscribe, the payer needs enough balance for roughly two days of outgoing payments plus the cost of a liquidation. They do not need to fund a full month upfront.
* A user can have up to 100 active subscriptions in one contract.

**Best for**

* Usage-based pricing: pay for exactly the time a service is used.
* AI agents paying for services continuously.
* High-frequency flows such as hourly DCA, where per-transaction billing would be too expensive.
* Payroll-like streams to a single recipient.

## Periodic (preview)

{% hint style="info" %}
Periodic subscriptions are in preview. Details may change before general availability.
{% endhint %}

In periodic mode a subscription has a **fixed amount per period**, for example $10 per month. This is the format finance teams and card subscriptions already use.

**How it works**

* Each periodic contract has a fixed period length, set at deployment (for example, monthly).
* The user subscribes with `subscribe(author, subscriptionAmount, projectId)`, where `subscriptionAmount` is the amount per period.
* **The first period is paid immediately**, at the moment of subscription. The author receives it right away.
* At the start of each following period, the period amount is deducted from the payer's balance. This happens through the same calculation as streaming, with no transaction. If two periods have passed since the last update, two period amounts are deducted.
* When the user cancels, the current period is not refunded. The subscription ends at the end of the period already paid.

**Requirements**

* The payer needs enough balance to cover the period amount plus a small reserve per subscription.

**Merchant notifications**

If the author is a smart contract, Papaya calls it when a subscription is created or cancelled (`streamCreated` and `streamRevoked` from `IPapayaNotification`). A merchant contract can use these calls to grant or revoke access automatically. If the author is a contract, it must implement this interface.

**Best for**

* Classic monthly subscriptions: SaaS, memberships, content, insurance premiums.
* Fintechs and wallets offering subscriptions to non-crypto users.

## Comparison

|                         | Streaming                   | Periodic (preview)                  |
| ----------------------- | --------------------------- | ----------------------------------- |
| Unit                    | Amount per second           | Amount per period                   |
| First payment           | Starts accruing immediately | Full period charged at subscription |
| Cancellation            | Stops immediately           | Current period is not refunded      |
| Balance needed to start | About 2 days of payments    | One full period                     |
| Transactions per period | None                        | None                                |
