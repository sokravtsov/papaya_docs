---
description: Basic setup of Papaya SDK - creating provider, signer and SDK instance
---

# Basic Setup

### Creating a Provider and Signer

First, you need to set up an Ethereum provider and (optionally) a signer:

```typescript
import { ethers } from 'ethers';

// Read-only provider
const provider = new ethers.JsonRpcProvider('https://polygon-rpc.com');

// For transactions, you need a signer
// Option 1: Using a private key (server-side)
const privateKey = 'YOUR_PRIVATE_KEY'; // Never hardcode this in production!
const signer = new ethers.Wallet(privateKey, provider);

// Option 2: Using a browser wallet like MetaMask (client-side)
// This assumes window.ethereum is available
const provider = new ethers.BrowserProvider(window.ethereum);
const signer = await provider.getSigner();
```

### Creating a Papaya SDK Instance

Once you have a provider or signer, you can create a Papaya SDK instance:

```typescript
import { 
  PapayaSDK, 
  RatePeriod, 
  formatInput, 
  formatOutput, 
  convertRateToPeriod 
} from '@papaya_fi/sdk';

// With a signer (for transactions)
const papaya = PapayaSDK.create(signer, 'polygon', 'USDT');

// Or with just a provider (for read-only operations)
const readOnlyPapaya = PapayaSDK.create(provider, 'polygon', 'USDT');
```

#### Parameters:

1. `provider` or `signer`: An ethers.js Provider or Signer
2. `network`: The blockchain network to use (default: 'polygon')
   * Available networks: 'polygon', 'bsc', 'avalanche', 'base', 'scroll', 'arbitrum', 'mainnet', 'sei', 'zksync'
3. `tokenSymbol`: The stablecoin to use (default: 'USDT')
   * Available tokens: 'USDT', 'USDC', 'PYUSD' (availability varies by network)
4. `contractVersion`: Optional contract version (defaults to the latest version for the selected network)
