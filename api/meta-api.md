---
description: >-
  Browser-compatible meta-transaction client for Papaya Gasless UX for
  subscriptions, payments, deposits & withdrawals – powered by EIP-712 and a
  relayer network.
---

# Meta API

> ✅ No axios – uses native fetch()
>
> ✅ Full EIP-712 signing (ethers-compatible)
>
> ✅ Non-custodial: user signs off-chain, relayer broadcasts on-chain
>
> ✅ Works in modern browsers and bundlers (Webpack, Vite, etc.)

***

### 📦 Installation & Initialization

```bash
npm install @papaya_fi/api ethers
```

```typescript
import { PapayaMetaApiClient } from '@papaya_fi/api/browser';

const metaClient = new PapayaMetaApiClient(
  'https://api.papaya.finance', // production endpoint
  'bsc-usdt',                   // 'bsc-usdc' | 'bsc-usdt' | 'pol-usdc'| 'pol-usdt'
  'your-api-key'                // issued after KYB and onboarding
);
```

#### Constructor Parameters

<table><thead><tr><th width="94">Param</th><th width="97">Required</th><th>Description</th></tr></thead><tbody><tr><td>baseUrl</td><td>✅</td><td>API base URL, e.g. 'https://api.papaya.finance'</td></tr><tr><td>contract</td><td>❌</td><td>Contract identifier: 'bsc-usdc' | 'bsc-usdt' | 'pol-usdc'| 'pol-usdt'</td></tr><tr><td>apiKey</td><td>✅</td><td>API key (issued by Papaya during onboarding)</td></tr><tr><td>provider</td><td>❌</td><td>Optional ethers.Provider, can be set later via .setProvider()</td></tr></tbody></table>

> 🔐 All requests automatically include the header: x-api-key: \<your-api-key>

***

### 🔑 Meta-Transaction Concept in Papaya

Meta-transactions allow users to perform operations without paying gas themselves:

1. Client → API: call prepare\*MetaTransaction(...) → get structured transactionData
2. Client → Wallet: call signMetaTransaction(...) → sign EIP-712 message with traits
3. Client → API: call executeMetaTransaction(...) → relayer submits the tx on-chain

Result: the user does not pay gas; they only pay according to your business logic (subscriptions, payments, etc.). Gas is paid by the relayer, which you or Papaya control.

***

### 📚 Method Overview

#### 1. Prepare Meta-Transactions (off-chain)

These methods prepare data for EIP-712 signing and later execution.

| Method                                                   | Params                                        | Returns                |                                                          |
| -------------------------------------------------------- | --------------------------------------------- | ---------------------- | -------------------------------------------------------- |
| prepareSubscriptionMetaTransaction(params)               | { from, author, subscriptionRate, projectId } | { from, method, data } | Prepares subscribe(...) call                             |
| prepareCancelSubscriptionMetaTransaction(author, params) | author, { from }                              | { from, method, data } | Prepares unsubscribe(author) call                        |
| preparePaymentMetaTransaction(params)                    | { from, to, amount }                          | from, method, data }   | Prepares pay(to, amount) call                            |
| prepareDepositMetaTransaction(params)                    | { from, amount, isPermit2? }                  | { from, method, data } | Prepares deposit(amount, isPermit2) call                 |
| prepareWithdrawMetaTransaction(params)                   | { from, amount, to? }                         | { from, method, data } | Prepares withdraw(amount) or withdrawTo(to, amount) call |

{% hint style="info" %}
📌 `amount` and `subscriptionRate` in token smallest units (wei-like). For USDT/USDC (18 decimals), multiply USD amount by 1e18: 50 USDT → '50000000000000000000'.\
\
📌 `amount` in `prepareDepositMetaTransaction()` in token should be same as for native token. \
example: **USDT** on **Polygon** (6 decimals), multiply USD amount by 1e6: 50 USDT → '50000000'.
{% endhint %}

***

#### 2. Signing (client-side, EIP-712)

**signMetaTransaction(transactionData, signer, contractAddress, chainId, relayerAddress)**

Signs prepared meta-transaction using EIP-712.

| Param           | Type          | Description                                            |
| --------------- | ------------- | ------------------------------------------------------ |
| transactionData | object        | Result of any prepare\*MetaTransaction() call          |
| signer          | ethers.Signer | Ethers signer, e.g. provider.getSigner() from MetaMask |
| contractAddress | string        | Papaya contract address (0x...)                        |
| chainId         | number        | Chain ID (e.g. 137 for Polygon)                        |
| relayerAddress  | string        | Address of the relayer (operated by you or Papaya)     |

Returns:

```typescript
{
  from: string;
  data: string;      // JSON string, e.g. { "data": "0x..." }
  nonce: number;
  signature: string; // EIP-712 signature
  deadline: number;  // unix timestamp
}
```

***

#### 3. Execute Meta-Transaction (via relayer)



**executeMetaTransaction(signedTransaction)**

Sends signed meta-transaction payload to the relayer API. The relayer then broadcasts the corresponding on-chain transaction.



Returns (typical):

* txHash: transaction hash after broadcast
* status: 'pending' | 'confirmed' | 'failed'
* On error – HTTP 4xx/5xx with error description



> ⚠️ The relayer must be authorized in the Papaya contract.
>
> Contact Papaya Team if you want to use the shared relayer or run your own.

***

### 🚀 Convenience “All-in-One” Methods



These helpers encapsulate: prepare → sign → execute.

<table><thead><tr><th>Method</th><th></th><th data-hidden></th></tr></thead><tbody><tr><td>createSubscriptionViaMetaTransaction(params, signer, contractAddress, chainId, relayerAddress)</td><td>Gasless subscription creation</td><td></td></tr><tr><td>cancelSubscriptionViaMetaTransaction(author, params, signer, contractAddress, chainId, relayerAddress)</td><td>Gasless subscription cancellation</td><td></td></tr><tr><td>makePaymentViaMetaTransaction(...)</td><td>Gasless one-off payment</td><td></td></tr><tr><td>depositFundsViaMetaTransaction(...)</td><td>Gasless deposit</td><td></td></tr><tr><td>withdrawFundsViaMetaTransaction(...)</td><td>Gasless withdraw</td><td></td></tr></tbody></table>

#### Example: Gasless Subscription

```typescript
import { ethers } from 'ethers';
import { PapayaMetaApiClient } from '@papaya_fi/api/browser';

const provider = new ethers.providers.Web3Provider(window.ethereum);
const signer = provider.getSigner();
const [account] = await provider.listAccounts();

const metaClient = new PapayaMetaApiClient(
  'https://api.papaya.finance',
  'pol-usdt',
  'your-api-key'
);

const result = await metaClient.createSubscriptionViaMetaTransaction(
  {
    from: account,
    author: '0x742d35Cc6634C0532925a3b8D4C9f2a93A9E3F1A',
    subscriptionRate: '50000000000000000000', // 50 USDT (18 decimals)
    projectId: 0
  },
  signer,
  '0x8F7d7e3F56c3A71E4f3B58A0E77a0A873c52bF05', // Papaya USDT contract
  137,                                          // Polygon
  '0xD9147F139980cFcB552Fcae2f3c9b7B215ACE850'  // Relayer address
);

console.log('Meta tx sent:', result.txHash);
```

***

### 🔁 Additional Methods

| Method                | Description                                                         |
| --------------------- | ------------------------------------------------------------------- |
| getNonce(address)     | Returns the current nonce for given address (for replay protection) |
| setProvider(provider) | Sets/updates ethers.Provider (useful to fetch chainId etc.)         |

***

### ⚠️ Important Notes

1.  Relayer security

    Only trusted relayers should be allowed to execute meta-transactions.

    Papaya can provide a shared relayer or help you deploy your own.
2.  Signature deadline

    Each meta-transaction has a deadline (unix timestamp). After that time, the contract rejects the signature.
3.  Replay protection

    Contracts validate (nonceType, nonce) pairs – each combination is unique and can be used only once.
4.  EIP-712 support

    Wallet must support eth\_signTypedData\_v4 (MetaMask, WalletConnect, Coinbase Wallet, etc.).

***

### 🛡️ Security & Compatibility

* ✅ Supports ethers.js v5 and v6
* ✅ Uses native fetch() only (no axios)
* ✅ Compatible with modern bundlers (Webpack, Vite, etc.)
* ✅ Relies on BigInt – runtime will check for availability
* ✅ Default HTTP timeout: 10 seconds for API calls

***

> 💡 Papaya protocol is non-custodial, audited, and stablecoin-native infrastructure for  payments and subscriptions &#x20;
