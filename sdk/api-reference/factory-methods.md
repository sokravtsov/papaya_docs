---
description: >-
  Factory methods of Papaya SDK for creating instances and getting network
  information
---

# Factory Methods

### `PapayaSDK.create()`

Creates a new instance of the Papaya SDK.

```typescript
static create(
  provider: ethers.Provider | ethers.Signer,
  network: NetworkName = 'polygon',
  tokenSymbol: TokenSymbol = 'USDT',
  contractVersion?: string
): PapayaSDK
```

**Parameters:**

* `provider`: An ethers.js Provider or Signer instance
* `network`: (Optional) The blockchain network to use (default: 'polygon')
* `tokenSymbol`: (Optional) The stablecoin to use (default: 'USDT')
* `contractVersion`: (Optional) Specific contract version to use (defaults to the latest version for the selected network)

**Returns:** A new `PapayaSDK` instance.

**Example:**

```typescript
const provider = new ethers.JsonRpcProvider('https://polygon-rpc.com');
const papaya = PapayaSDK.create(provider, 'polygon', 'USDT');
```

### `PapayaSDK.getAvailableNetworks()`

Returns a list of all networks supported by the SDK.

```typescript
static getAvailableNetworks(): NetworkName[]
```

**Returns:** Array of network names.

**Example:**

```typescript
const networks = PapayaSDK.getAvailableNetworks();
console.log(networks); // ['polygon', 'bsc', 'avalanche', ...]
```

### `PapayaSDK.getAvailableTokens()`

Returns a list of tokens available for a specific network.

```typescript
static getAvailableTokens(network: NetworkName): TokenSymbol[]
```

**Parameters:**

* `network`: The network to check for available tokens

**Returns:** Array of token symbols available on the specified network.

**Example:**

```typescript
const tokens = PapayaSDK.getAvailableTokens('polygon');
console.log(tokens); // ['USDT', 'USDC']
```
