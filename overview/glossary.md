---
description: Key terms used in Papaya docs.
---

# Glossary

**Author.** The recipient of a subscription: a merchant, creator or service.

**Balance.** The amount a user holds inside a Papaya contract, in the deposited stablecoin.

**Deposit.** Moving stablecoins from a wallet into a Papaya balance.

**depositFor.** A deposit made by one address into another user's balance.

**Keeper.** A service that calls `liquidate` on accounts that need a refill or liquidation.

**Liquidation.** What happens when an account cannot cover its subscriptions and cannot be refilled: all its subscriptions are cancelled and the caller is rewarded.

**Meta-transaction.** A transaction signed by the user and submitted by a relayer, who pays the gas.

**Period.** In periodic mode, the fixed length of one billing cycle, for example one month.

**Periodic subscription.** A subscription with a fixed amount per period, charged at the start of each period.

**Project.** A platform or merchant group inside Papaya, with an ID, an admin and an optional fee.

**Project fee.** The share of each subscription that goes to the project owner, up to 20%.

**Rate.** In streaming mode, the amount paid per second.

**Refill.** Pulling funds from a user's wallet into their Papaya balance when it runs low, using the allowance the user has given.

**Relayer.** A service that submits signed transactions onchain and pays the gas.

**Streaming subscription.** A subscription where value moves continuously, second by second.
