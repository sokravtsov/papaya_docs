---
description: Short answers to common questions.
---

# FAQ

**Does Papaya send a transaction every time a subscription is charged?** No. Balances are calculated from rates and time. There is no transaction per period, no matter how often the subscription is charged.

**Does the user need to deposit money first?** Yes. Subscriptions draw from the user's Papaya balance. The balance can be funded by the user, by a partner with `depositFor`, or refilled automatically from the user's wallet if they have given an allowance.

**Does Papaya hold user funds?** Funds sit in the Papaya smart contract until they are withdrawn. Papaya does not hold private keys, and the contract owner cannot move user balances. Users and merchants can withdraw at any time.

**Do users need a gas token?** For transactions they send themselves, yes. With a relayer, no: the user signs and the relayer pays the gas. On networks like Arc, gas is paid in USDC.

**What happens if a user runs out of balance?** Papaya tries to refill from the user's wallet. If that is not possible, the user's subscriptions are cancelled. See [Balance, refill and liquidation](balance-refill-and-liquidation.md).

**Is there a grace period or retry?** No. If a refill fails, the subscription stops. Reminders and retry logic can be built off-chain by the merchant or a partner.

**Can a user get a refund when they cancel?** In streaming mode, payment stops the moment the user cancels, so there is nothing to refund. In periodic mode, the current period is not refunded.

**Is there a separate contract for each merchant?** No. There is one Papaya contract per stablecoin per network. Merchants and platforms are identified by a project ID and their own address.

**Does Papaya issue a token?** No. Balances are held in the stablecoin the user deposited. The internal balance (for example ppUSDC) is an accounting unit inside the contract, always backed one to one by the deposited stablecoin.

**Does Papaya handle invoices, tax or fiat payouts?** No. Papaya is the recurring payment rail. Invoicing, tax and fiat settlement are handled by the merchant or a partner.

**Can Papaya be used for payouts to many recipients?** Papaya is built for recurring payments from many payers. For one-to-many payouts, each recipient is a separate subscription or payment.

**Which networks are supported?** See [Supported networks](supported-networks.md). New EVM networks can usually be added within a day.

**How do I integrate?** Start with the [SDK](../sdk/overview.md). For gasless flows, see the [Meta API](../api/meta-api.md).
