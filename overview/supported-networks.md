---
description: Networks, stablecoins and network-specific notes.
---

# Supported networks

Papaya runs on EVM networks. Each contract supports one stablecoin on one network.

## Live

| Network   | Stablecoins            |
| --------- | ---------------------- |
| Ethereum  | USDC, USDT, PYUSD, DAI |
| BNB Chain | USDC, USDT             |
| Polygon   | USDC, USDT             |
| Base      | USDC                   |
| Arbitrum  | USDC, USDT             |
| Avalanche | USDC, USDT             |
| Scroll    | USDC, USDT             |
| Sei       | USDC, USDT             |
| zkSync    | USDT                   |
| Arc       | USDC                   |

Contract addresses and versions for each network are listed in the [SDK network support](../sdk/network-support/) section.

## New networks

Papaya can be deployed on any EVM network with a supported stablecoin, usually within a day. If you need Papaya on a network not listed here, contact the team.

## Network notes

* **Gas cost.** On L2s and payment networks, Papaya transactions cost a fraction of a cent. On Ethereum mainnet they are more expensive, and this is where the fact that Papaya does not send a transaction per period saves the most.
* **Keepers.** Refill and liquidation rewards are designed to cover gas on low-cost networks. On Ethereum mainnet, plan to run a partner or Papaya keeper.
* **Arc.** Gas on Arc is paid in USDC, so users do not need a separate gas token.
