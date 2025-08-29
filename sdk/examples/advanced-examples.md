---
description: Advanced examples and patterns for Papaya SDK
---

# Advanced Examples

{% hint style="info" %}
This document covers advanced usage patterns and sophisticated integrations with the Papaya SDK.
{% endhint %}

### Gas Optimization

#### Batching Transactions

If you need to perform multiple operations, consider batching them to minimize gas costs:

```typescript
import { ethers } from 'ethers';
import { PapayaSDK } from '@papaya_fi/sdk';

async function optimizedOperations(signer: ethers.Signer) {
  const papaya = PapayaSDK.create(signer, 'polygon', 'USDT');
  
  // Instead of multiple separate transactions:
  // await papaya.deposit(100);
  // await papaya.subscribe(creator1, 10);
  // await papaya.subscribe(creator2, 5);
  
  // Batch the operations in your UI/UX flow
  // First deposit enough tokens for everything
  const depositTx = await papaya.deposit(115); // 100 + 10 + 5
  await depositTx.wait();
  
  // Then do the subscriptions
  const [tx1, tx2] = await Promise.all([
    papaya.subscribe(creator1, 10),
    papaya.subscribe(creator2, 5)
  ]);
  
  await Promise.all([tx1.wait(), tx2.wait()]);
}
```

#### Using Permit2 for Deposits

The Papaya SDK supports using Permit2 for approving and depositing tokens in a single transaction, which saves gas:

```typescript
import { PapayaSDK } from '@papaya_fi/sdk';

async function depositWithPermit2(papaya: PapayaSDK, amount: number) {
  // Set isPermit2 to true to use Permit2 for approval and deposit in one transaction
  const tx = await papaya.deposit(amount, true);
  await tx.wait();
  console.log('Deposit with Permit2 completed successfully');
}
```

### Working with Custom Contract Versions

The Papaya SDK supports multiple contract versions for each network and token.

#### Specifying a Contract Version

```typescript
import { PapayaSDK } from '@papaya_fi/sdk';

// Using a specific contract version
const papayaV1 = PapayaSDK.create(provider, 'polygon', 'USDT', '1');

// Using the latest version (default)
const papaya = PapayaSDK.create(provider, 'polygon', 'USDT');
```

#### Working with Custom Contracts

You can also specify custom contract and token addresses:

```typescript
import { PapayaSDK, PapayaSDKOptions } from '@papaya_fi/sdk';

// Using custom addresses
const options: PapayaSDKOptions = {
  provider: signer,
  network: 'polygon',
  tokenSymbol: 'USDT',
  contractAddress: '0xCustomContractAddress',
  tokenAddress: '0xCustomTokenAddress'
};

const papaya = new PapayaSDK(options);
```

### Multiple Network Support

#### Working with Multiple Networks Simultaneously

For applications that need to work with multiple networks, you can create multiple SDK instances:

```typescript
import { ethers } from 'ethers';
import { PapayaSDK, NetworkName } from '@papaya_fi/sdk';

// Function to create SDK instances for multiple networks
async function createMultiNetworkSDKs(privateKey: string) {
  const networks: NetworkName[] = ['polygon', 'bsc', 'mainnet'];
  const sdkInstances = {};
  
  for (const network of networks) {
    // Create provider for each network
    const provider = new ethers.JsonRpcProvider(getRpcUrl(network));
    const signer = new ethers.Wallet(privateKey, provider);
    
    // Create SDK instance
    sdkInstances[network] = PapayaSDK.create(signer, network, 'USDT');
  }
  
  return sdkInstances;
}

// Helper function to get RPC URL for a network
function getRpcUrl(network: NetworkName): string {
  const rpcUrls = {
    polygon: 'https://polygon-rpc.com',
    bsc: 'https://bsc-dataseed.binance.org',
    mainnet: 'https://eth.llamarpc.com',
    // Add more networks as needed
  };
  
  return rpcUrls[network] || rpcUrls['polygon']; // Default to polygon
}
```

#### Dynamically Switching Networks

For applications that need to switch networks dynamically:

```typescript
import { ethers } from 'ethers';
import { PapayaSDK, NetworkName, TokenSymbol } from '@papaya_fi/sdk';

class NetworkManager {
  private signer: ethers.Signer;
  private currentSDK: PapayaSDK | null = null;
  private currentNetwork: NetworkName | null = null;
  
  constructor(signer: ethers.Signer) {
    this.signer = signer;
  }
  
  async switchNetwork(network: NetworkName, token: TokenSymbol = 'USDT') {
    if (network === this.currentNetwork) return this.currentSDK;
    
    try {
      // For browser wallet integration, you might need to request network switch
      if (window.ethereum) {
        const chainId = getChainId(network);
        await window.ethereum.request({
          method: 'wallet_switchEthereumChain',
          params: [{ chainId: `0x${chainId.toString(16)}` }],
        });
      }
      
      // Create new SDK instance for the selected network
      this.currentSDK = PapayaSDK.create(this.signer, network, token);
      this.currentNetwork = network;
      
      return this.currentSDK;
    } catch (error) {
      console.error(`Error switching to network ${network}:`, error);
      throw error;
    }
  }
  
  getCurrentSDK(): PapayaSDK {
    if (!this.currentSDK) {
      throw new Error('No network selected. Call switchNetwork first.');
    }
    return this.currentSDK;
  }
}

// Helper function to get chain ID for a network
function getChainId(network: NetworkName): number {
  const chainIds = {
    polygon: 137,
    bsc: 56,
    avalanche: 43114,
    base: 8453,
    scroll: 534352,
    arbitrum: 42161,
    mainnet: 1,
    sei: 32741,
    zksync: 324
  };
  
  return chainIds[network] || 137; // Default to polygon
}
```

### Relayer Services

To fully leverage **BySig methods**, you'll need a relayer service to submit the signed transactions to the blockchain.

#### Building a Simple Relayer

Here's a basic example of how to build a simple relayer service using **Node.js** and **Express**:

```typescript
// relayer.ts
import express from 'express';
import { ethers } from 'ethers';
import { PapayaSDK } from '@papaya_fi/sdk';
import dotenv from 'dotenv';

dotenv.config();

const app = express();
app.use(express.json());

const NETWORKS = {
  polygon: 'https://polygon-rpc.com',
  bsc: 'https://bsc-dataseed.binance.org',
  mainnet: 'https://eth.llamarpc.com',
  // Add more networks as needed
};

// Initialize providers and signers for each network
const providers = {};
const signers = {};
const sdkInstances = {};

Object.entries(NETWORKS).forEach(([network, rpcUrl]) => {
  providers[network] = new ethers.JsonRpcProvider(rpcUrl);
  signers[network] = new ethers.Wallet(process.env.RELAYER_PRIVATE_KEY, providers[network]);
  sdkInstances[network] = PapayaSDK.create(signers[network], network as any, 'USDT');
});

// Endpoint to handle gasless deposits
app.post('/api/relay/deposit', async (req, res) => {
  try {
    const { txData, chainId } = req.body;
    
    // Determine network from chain ID
    const network = getNetworkFromChainId(chainId);
    if (!network || !sdkInstances[network]) {
      return res.status(400).json({ 
        success: false, 
        error: 'Unsupported network' 
      });
    }
    
    // Submit the transaction
    const provider = providers[network];
    const signer = signers[network];
    
    // Here you would extract the necessary data from txData
    // and call the contract's bySig method directly
    
    // For a complete implementation, you would:
    // 1. Extract user address, amount, deadline, and signature from txData
    // 2. Call the contract directly with these parameters
    // 3. Return the transaction hash
    
    // Simplified example (this is not complete and would need adaptation):
    const tx = await signer.sendTransaction(txData);
    const receipt = await tx.wait();
    
    return res.json({
      success: true,
      txHash: receipt.hash
    });
  } catch (error) {
    console.error('Relayer error:', error);
    return res.status(500).json({
      success: false,
      error: 'Relayer error: ' + error.message
    });
  }
});

function getNetworkFromChainId(chainId: number): string | null {
  const chainIdMap = {
    1: 'mainnet',
    56: 'bsc',
    137: 'polygon',
    // Add more as needed
  };
  
  return chainIdMap[chainId] || null;
}

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Relayer service running on port ${PORT}`);
});
```

### Error Handling and Recovery

#### Common Errors and Solutions

| Error                     | Potential Cause                               | Solution                                                      |
| ------------------------- | --------------------------------------------- | ------------------------------------------------------------- |
| "Insufficient allowance"  | Token approval needed                         | Call the token's approve method before depositing             |
| "Insufficient balance"    | User doesn't have enough tokens               | Inform user to get more tokens                                |
| "Transaction underpriced" | Gas price too low                             | Increase gas price or wait for network congestion to decrease |
| "Nonce too low"           | Transaction with same nonce already processed | Reset nonce or use the next available nonce                   |
| "Deadline expired"        | BySig transaction submitted after deadline    | Generate a new signature with a future deadline               |

#### Implementing Robust Error Handling

```typescript
import { PapayaSDK } from '@papaya_fi/sdk';
import { ethers } from 'ethers';

async function robustDeposit(papaya: PapayaSDK, amount: number): Promise<boolean> {
  try {
    const tx = await papaya.deposit(amount);
    await tx.wait();
    return true;
  } catch (error) {
    // Handle specific errors
    if (error.message.includes('insufficient allowance')) {
      console.warn('Token approval needed. Attempting to approve...');
      try {
        // Attempt to approve tokens and retry
        // This would require implementing an approveTokens function
        await approveTokens(papaya, amount);
        
        // Retry deposit
        const tx = await papaya.deposit(amount);
        await tx.wait();
        return true;
      } catch (approvalError) {
        console.error('Failed to approve tokens:', approvalError);
        throw new Error('Token approval failed. Please approve tokens manually.');
      }
    } else if (error.message.includes('insufficient funds')) {
      throw new Error('Insufficient balance. Please add more tokens to your wallet.');
    } else {
      // Generic error handling
      console.error('Deposit error:', error);
      throw error;
    }
  }
}

// Example function to approve tokens (implementation would depend on your setup)
async function approveTokens(papaya: PapayaSDK, amount: number) {
  // Implementation would depend on how you access the token contract
  // This is just a placeholder
  const tokenContract = getTokenContract();
  const tx = await tokenContract.approve(papaya.getContractAddress(), amount);
  await tx.wait();
}
```

#### Transaction Monitoring and Recovery

For critical operations, implement transaction monitoring and recovery:

```typescript
import { PapayaSDK } from '@papaya_fi/sdk';
import { ethers } from 'ethers';

async function monitorTransaction(
  txHash: string,
  provider: ethers.Provider,
  maxAttempts: number = 10
): Promise<ethers.TransactionReceipt> {
  let attempts = 0;
  
  while (attempts < maxAttempts) {
    try {
      const receipt = await provider.getTransactionReceipt(txHash);
      
      if (receipt) {
        // Check if transaction was successful
        if (receipt.status === 1) {
          return receipt;
        } else {
          throw new Error('Transaction failed');
        }
      }
      
      // Wait before checking again
      await new Promise(resolve => setTimeout(resolve, 5000));
      attempts++;
    } catch (error) {
      if (attempts >= maxAttempts) {
        throw error;
      }
      
      // Wait longer before retrying
      await new Promise(resolve => setTimeout(resolve, 5000));
      attempts++;
    }
  }
  
  throw new Error('Transaction not confirmed after maximum attempts');
}

// Usage example
async function safeDeposit(papaya: PapayaSDK, amount: number) {
  try {
    const tx = await papaya.deposit(amount);
    console.log(`Transaction sent: ${tx.hash}`);
    
    // Monitor transaction
    const receipt = await monitorTransaction(tx.hash, papaya.getProvider());
    console.log(`Deposit confirmed in block ${receipt.blockNumber}`);
    
    return receipt;
  } catch (error) {
    console.error('Deposit failed:', error);
    // Implement recovery logic here if needed
    throw error;
  }
}
```

### Performance Optimization

#### Caching Strategies

```typescript
class CachedPapayaSDK {
  private papaya: PapayaSDK;
  private cache: Map<string, { data: any; timestamp: number }> = new Map();
  private cacheTimeout: number = 30000; // 30 seconds
  
  constructor(papaya: PapayaSDK) {
    this.papaya = papaya;
  }
  
  async getCachedBalance(address: string): Promise<string> {
    const cacheKey = `balance_${address}`;
    const cached = this.cache.get(cacheKey);
    
    if (cached && Date.now() - cached.timestamp < this.cacheTimeout) {
      return cached.data;
    }
    
    const balance = await this.papaya.balanceOf(address);
    this.cache.set(cacheKey, { data: balance, timestamp: Date.now() });
    
    return balance;
  }
  
  async getCachedUserInfo(address: string): Promise<any> {
    const cacheKey = `userInfo_${address}`;
    const cached = this.cache.get(cacheKey);
    
    if (cached && Date.now() - cached.timestamp < this.cacheTimeout) {
      return cached.data;
    }
    
    const userInfo = await this.papaya.getUserInfo(address);
    this.cache.set(cacheKey, { data: userInfo, timestamp: Date.now() });
    
    return userInfo;
  }
  
  // Clear cache when transactions are made
  clearCache() {
    this.cache.clear();
  }
}
```

_These advanced techniques will help you build robust applications that leverage the full power of the Papaya SDK while ensuring optimal performance and user experience._
