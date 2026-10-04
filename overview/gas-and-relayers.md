---
description: Who pays gas and how gasless transactions work.
---

# Gas and relayers

## Who pays gas

| Action                                    | Who pays                                                      |
| ----------------------------------------- | ------------------------------------------------------------- |
| Deposit, subscribe, cancel, withdraw, pay | The user, in the network's gas token. Or a relayer, see below |
| Accrual each second or period             | Nobody, there is no transaction                               |
| Refill                                    | The caller pays gas and is compensated from the refill        |
| Liquidation                               | The caller pays gas and receives the liquidation reward       |
| Merchant withdrawal                       | The merchant                                                  |

On networks where gas is paid in a stablecoin, such as Arc (USDC), users do not need a second asset to pay for gas.

## Gasless transactions with a relayer

Papaya supports signed transactions (EIP-712). A user signs an action in their wallet, and a relayer submits it onchain and pays the gas. Supported actions include subscribe, unsubscribe, deposit, withdraw and one-off payments. See the [Meta API](../api/meta-api.md).

**Who pays the relayer**

This is set per deployment. The gas can be covered by:

* a partner or payment provider,
* the merchant,
* Papaya, with the cost included in the overall fee.

A relayer can also be compensated in stablecoins from the signer's Papaya balance, if the signed transaction includes this.

With a relayer, end users can subscribe and pay without ever holding the network's gas token.

## Batching

Several actions can be combined in one transaction with `multicall`, for example deposit and subscribe together. Signed actions from different users can also be submitted together by a relayer. Each action still updates its own account, so batching saves transaction overhead, not per-user work.

## Typical gas usage

Measured on Polygon (median):

| Action                            | Gas       |
| --------------------------------- | --------- |
| Deposit                           | \~74,000  |
| Subscribe                         | \~236,000 |
| Unsubscribe                       | \~129,000 |
| Withdraw                          | \~110,000 |
| Deposit and subscribe (multicall) | \~269,000 |

The full lifecycle of a subscriber (deposit, subscribe, cancel) is about 440,000 gas, regardless of how many periods the subscription runs. On most L2s and payment networks this is a fraction of a cent.
