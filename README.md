---
description: >-
  Recurring stablecoin payments where cost does not grow with the number of
  periods.
---

# Introduction

Papaya is a protocol for recurring payments in stablecoins.

A subscription is opened once onchain and keeps running until it is changed or cancelled. Nobody has to send a new transaction every month, every day or every minute to keep it going. The cost of a subscription does not grow with the number of periods it runs.

Papaya supports two subscription modes:

* **Streaming.** Value moves continuously, second by second. Good for usage-based pricing, AI agents and high-frequency flows like hourly DCA.
* **Periodic**. A fixed amount per period, charged at the start of the period, the way a card subscription works. $10 this month, $10 next month.

Both modes run on the same principles: a user funds a balance in the Papaya contract, subscriptions draw from that balance, and the merchant withdraws what has accrued whenever they want.

## Why Papaya

**Cost does not depend on frequency.** Most onchain billing sends one transaction per charge. Monthly billing means 12 transactions a year per customer, hourly billing means 8,760. Papaya calculates balances from rates and time, so there is no transaction per period at all. A user pays gas only when they do something: deposit, subscribe, cancel, withdraw.

**Non-custodial.** Papaya never holds user keys. Users and merchants can withdraw their balance at any time. The contract owner cannot move user funds.

**Works on any EVM network.** The same protocol runs on Ethereum, BNB Chain, Polygon, Base, Arbitrum, Avalanche, Arc and other EVM networks. New networks can be added quickly.

**Your stablecoin, no new asset.** Balances are held in the stablecoin the user deposited (USDC, USDT, PYUSD and others). Inside the contract they are tracked as an internal balance (for example ppUSDC), always backed one to one. Papaya does not create a new token standard.

## Who it is for

* **Fintechs, wallets and payment providers** that already move stablecoins and want to add recurring payments for their users.
* **Crypto-native products** that need subscriptions or usage-based billing.
* **AI agent platforms** that need agents to pay for services continuously and within limits.
* **DCA and investment products** that need automated, high-frequency purchases.

## What Papaya is not

Papaya is the recurring payment rail. It is not a full billing system. Invoicing, tax and fiat settlement are handled by the merchant or by a partner.

## Next steps

* [How it works](overview/how-it-works.md)
* [Subscription modes](overview/subscription-modes.md)
* [Supported networks](overview/supported-networks.md)
* For developers: [SDK overview](sdk/overview.md) and [Protocol reference](<README (1).md>)

