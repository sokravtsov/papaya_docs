---
description: Supported blockchain networks in Papaya SDK
---

# Supported Networks

The SDK currently supports the following networks:

| Network     | Chain ID | Description                                                 |
| ----------- | -------- | ----------------------------------------------------------- |
| `polygon`   | 137      | Polygon mainnet, a popular Ethereum scaling solution        |
| `bsc`       | 56       | Binance Smart Chain, Binance's EVM-compatible blockchain    |
| `avalanche` | 43114    | Avalanche C-Chain, an EVM-compatible blockchain             |
| `base`      | 8453     | Base, an Ethereum L2 scaling solution by Coinbase           |
| `scroll`    | 534352   | Scroll, an Ethereum L2 zk-rollup scaling solution           |
| `arbitrum`  | 42161    | Arbitrum, an Ethereum L2 optimistic rollup scaling solution |
| `mainnet`   | 1        | Ethereum mainnet                                            |
| `sei`       | 32741    | Sei EVM, a high-performance EVM-compatible blockchain       |
| `zksync`    | 324      | zkSync Era, an Ethereum L2 zk-rollup scaling solution       |

You can get a list of all supported networks programmatically:

```typescript
import { PapayaSDK } from '@papaya_fi/sdk';

const networks = PapayaSDK.getAvailableNetworks();
console.log(networks);
```

### RPC Providers

To use the Papaya SDK, you'll need access to an RPC endpoint for the network you're targeting. Here are some public RPC endpoints for the supported networks:

| Network   | Example RPC URL                         |
| --------- | --------------------------------------- |
| polygon   | `https://polygon-rpc.com`               |
| bsc       | `https://bsc-dataseed.binance.org`      |
| avalanche | `https://api.avax.network/ext/bc/C/rpc` |
| base      | `https://mainnet.base.org`              |
| scroll    | `https://rpc.scroll.io`                 |
| arbitrum  | `https://arb1.arbitrum.io/rpc`          |
| mainnet   | `https://eth.llamarpc.com`              |
| sei       | `https://evm-rpc.sei.io`                |
| zksync    | `https://mainnet.era.zksync.io`         |

_For production use, we recommend using a dedicated RPC provider service like_ [_Infura_](https://www.infura.io/)_,_ [_Alchemy_](https://www.alchemy.com/)_, or_ [_QuickNode_](https://www.quicknode.com/)_._
