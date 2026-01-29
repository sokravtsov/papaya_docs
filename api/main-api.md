---
description: >-
  Browser-compatible JavaScript API client for Papaya crypto payments,
  subscriptions, and revenue splits with no axios dependency.
---

# Main API

✅ Works in modern browsers

✅ Uses native fetch()

✅ Non-custodial, signer-based transaction execution

✅ Supports USDT/USDC on Ethereum and L2s (Arbitrum, Base, etc.)

***

### 📦 Installation

```
npm install @papaya_fi/api ethers
```

### Features

* Simple interface for interacting with the Papaya Protocol
* Support for multiple networks (Ethereum, Base, Polygon, BSC, Avalanche, etc.)
* Multiple stablecoin support (USDT, USDC, PYUSD)
* Typed definitions for better development experience
* Multiple contract version support
* BySig methods for gasless transactions
* Comprehensive transaction handling
* Utility functions for rate conversions and data formatting

### Quick Start

```typescript
import { ethers } from 'ethers';
import { PapayaSDK, formatOutput, convertRateToPeriod, RatePeriod } from '@papaya_fi/sdk';

// Create an Ethereum provider
const provider = new ethers.JsonRpcProvider('YOUR_RPC_URL');

// Create a signer if you need to send transactions
const privateKey = 'YOUR_PRIVATE_KEY';
const signer = new ethers.Wallet(privateKey, provider);

// Create a Papaya SDK instance
const papaya = PapayaSDK.create(
  signer,      // Or provider if you only need read-only operations
  'polygon',   // Network name (default is 'polygon')
  'USDT'       // Token symbol (default is 'USDT')
);

// Now you can use the SDK to interact with the Papaya Protocol
async function getBalance() {
  const rawBalance = await papaya.balanceOf();
  // Convert raw balance to readable format
  const readableBalance = formatOutput(BigInt(rawBalance), 18);
  console.log(`Your balance: ${readableBalance} USDT`);
}

// Example subscription
async function subscribeToAuthor() {
  const authorAddress = '0x...';  // The address to subscribe to
  const amountPerMonth = 10;      // Amount in tokens per month
  
  const tx = await papaya.subscribe(authorAddress, amountPerMonth);
  await tx.wait();
  console.log('Successfully subscribed!');
}

// Example getting user info with rate conversion
async function getUserInfo() {
  const userInfo = await papaya.getUserInfo();
  
  // Convert raw blockchain data to human-readable format
  const formattedInfo = {
    balance: formatOutput(BigInt(userInfo.balance), 18),
    // Convert per-second rates to monthly rates
    incomeRate: convertRateToPeriod(Number(formatOutput(userInfo.incomeRate, 18)), RatePeriod.MONTH),
    outgoingRate: convertRateToPeriod(Number(formatOutput(userInfo.outgoingRate, 18)), RatePeriod.MONTH),
    updated: new Date(Number(userInfo.updated) * 1000).toISOString()
  };
  
  console.log(`Balance: ${formattedInfo.balance} USDT`);
  console.log(`Monthly income: ${formattedInfo.incomeRate} USDT`);
  console.log(`Monthly outgoing: ${formattedInfo.outgoingRate} USDT`);
}
```

### Support

For questions, issues or feature requests, please open an issue on our GitHub repository or contact us at [Papaya Community](https://t.me/PapayaCommunity/26037).

### Jump right in

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h4><i class="fa-rocket-launch">:rocket-launch:</i></h4></td><td><strong>Getting Started</strong></td><td></td><td></td><td><a href="../sdk/getting-started/">getting-started</a></td></tr><tr><td><h4><i class="fa-webhook">:webhook:</i></h4></td><td><strong>API Reference</strong></td><td></td><td></td><td><a href="../sdk/api-reference/">api-reference</a></td></tr><tr><td><h4><i class="fa-lightbulb">:lightbulb:</i></h4></td><td><strong>Examples</strong></td><td></td><td></td><td><a href="../sdk/examples/">examples</a></td></tr><tr><td><h4><i class="fa-chart-network">:chart-network:</i></h4></td><td><strong>Network Support</strong></td><td></td><td></td><td><a href="../sdk/network-support/">network-support</a></td></tr><tr><td><h4><i class="fa-shapes">:shapes:</i></h4></td><td><strong>Utilities</strong></td><td></td><td></td><td><a href="../sdk/utilities/">utilities</a></td></tr></tbody></table>
