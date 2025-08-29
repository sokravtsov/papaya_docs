---
description: Token availability across different networks in Papaya SDK
---

# Token Availability

{% hint style="info" %}
The SDK supports the following stablecoin tokens:
{% endhint %}

| Token   | Description                                                          |
| ------- | -------------------------------------------------------------------- |
| `USDT`  | Tether USD, a widely used stablecoin                                 |
| `USDC`  | USD Coin, a fully-collateralized stablecoin                          |
| `PYUSD` | PayPal USD, a stablecoin issued by PayPal (only on Ethereum mainnet) |

{% hint style="info" %}
Not all tokens are available on all networks. You can check which tokens are available on a specific network:
{% endhint %}

```typescript
import { PapayaSDK } from '@papaya_fi/sdk';

const polygonTokens = PapayaSDK.getAvailableTokens('polygon');
console.log(polygonTokens); // ['USDT', 'USDC']
```

### Network and Token Availability Matrix

Below is a matrix showing which tokens are available on which networks:

| Network   | USDT | USDC | PYUSD |
| --------- | ---- | ---- | ----- |
| polygon   | ✅    | ✅    | ❌     |
| bsc       | ✅    | ✅    | ❌     |
| avalanche | ✅    | ✅    | ❌     |
| base      | ❌    | ✅    | ❌     |
| scroll    | ✅    | ✅    | ❌     |
| arbitrum  | ✅    | ✅    | ❌     |
| mainnet   | ✅    | ✅    | ✅     |
| sei       | ✅    | ✅    | ❌     |
| zksync    | ✅    | ❌    | ❌     |

### Contract Versions

The SDK supports multiple contract versions for each token on each network. By default, it will use the latest available version, but you can specify a particular version if needed.

_For example, on Polygon, both USDT and USDC have versions "1" and "1.5.3" available._

When creating a new SDK instance, you can specify a particular version:

```typescript
import { PapayaSDK } from '@papaya_fi/sdk';

// Using the latest version (default)
const papaya = PapayaSDK.create(provider, 'polygon', 'USDT');

// Specifying a particular version
const papayaV1 = PapayaSDK.create(provider, 'polygon', 'USDT', '1');
```
