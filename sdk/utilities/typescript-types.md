---
description: TypeScript types and interfaces of Papaya SDK
---

# TypeScript Types

{% hint style="info" %}
The Papaya SDK provides full TypeScript typing for better development experience and autocompletion.
{% endhint %}

### Main Types

### `PapayaSDK`

The main SDK class for interacting with the Papaya Protocol.

```typescript
class PapayaSDK {
  static create(
    provider: ethers.Provider | ethers.Signer,
    network?: NetworkName,
    tokenSymbol?: TokenSymbol,
    contractVersion?: string
  ): PapayaSDK;
  
  static getAvailableNetworks(): NetworkName[];
  static getAvailableTokens(network: NetworkName): TokenSymbol[];
}
```

### `NetworkName`

Type for supported network names.

```typescript
type NetworkName = 
  | 'polygon'
  | 'bsc'
  | 'avalanche'
  | 'base'
  | 'scroll'
  | 'arbitrum'
  | 'mainnet'
  | 'sei'
  | 'zksync';
```

### `TokenSymbol`

Type for supported token symbols.

```typescript
type TokenSymbol = 'USDT' | 'USDC' | 'PYUSD';
```

### `RatePeriod`

Enum for time periods of rates.

```typescript
enum RatePeriod {
  SECOND = 'second',
  HOUR = 'hour',
  DAY = 'day',
  WEEK = 'week',
  MONTH = 'month',
  YEAR = 'year'
}
```

### Data Interfaces

### `UserInfo`

Interface for user information.

```typescript
interface UserInfo {
  balance: bigint;
  incomeRate: bigint;
  outgoingRate: bigint;
  updated: bigint;
}
```

### `Subscription`

Interface for subscription information.

```typescript
interface Subscription {
  recipient: string;
  incomeRate: bigint;
  outgoingRate: bigint;
  projectId: number;
}
```

### `SubscriptionInfo`

Interface for detailed subscription information.

```typescript
interface SubscriptionInfo {
  isSubscribed: boolean;
  outgoingRate: bigint;
  projectId: number;
}
```

### Type Usage Examples

#### Creating a Typed Instance

```typescript
import { PapayaSDK, NetworkName, TokenSymbol } from '@papaya_fi/sdk';

// Typed parameters
const network: NetworkName = 'polygon';
const token: TokenSymbol = 'USDT';

const papaya = PapayaSDK.create(provider, network, token);
```

#### Working with User Information

```typescript
import { UserInfo, formatOutput, convertRateToPeriod, RatePeriod } from '@papaya_fi/sdk';

async function displayUserInfo() {
  const userInfo: UserInfo = await papaya.getUserInfo();
  
  const formattedInfo = {
    balance: formatOutput(userInfo.balance, 18),
    incomeRate: convertRateToPeriod(
      Number(formatOutput(userInfo.incomeRate, 18)), 
      RatePeriod.MONTH
    ),
    outgoingRate: convertRateToPeriod(
      Number(formatOutput(userInfo.outgoingRate, 18)), 
      RatePeriod.MONTH
    ),
    updated: new Date(Number(userInfo.updated) * 1000)
  };
  
  return formattedInfo;
}
```

#### Working with Subscriptions

```typescript
import { Subscription, convertRateToPeriod, RatePeriod } from '@papaya_fi/sdk';

async function getFormattedSubscriptions() {
  const subscriptions: Subscription[] = await papaya.getSubscriptions();
  
  return subscriptions.map((sub: Subscription) => ({
    recipient: sub.recipient,
    monthlyRate: convertRateToPeriod(
      Number(formatOutput(sub.outgoingRate, 18)), 
      RatePeriod.MONTH
    ),
    projectId: sub.projectId
  }));
}
```

#### Checking Subscriptions

```typescript
import { SubscriptionInfo } from '@papaya_fi/sdk';

async function checkSubscription(creatorAddress: string) {
  const subInfo: SubscriptionInfo = await papaya.isSubscribed(creatorAddress);
  
  if (subInfo.isSubscribed) {
    const monthlyRate = convertRateToPeriod(
      Number(formatOutput(subInfo.outgoingRate, 18)), 
      RatePeriod.MONTH
    );
    console.log(`Subscribed to ${creatorAddress} with rate ${monthlyRate} USDT/month`);
  } else {
    console.log(`Not subscribed to ${creatorAddress}`);
  }
}
```

### Utility Types

### `BigNumberish`

Type for numbers that can be converted to BigNumber.

```typescript
type BigNumberish = string | number | bigint;
```

### `TransactionResponse`

Type for ethers.js transaction responses.

```typescript
import { TransactionResponse } from 'ethers';

async function sendTransaction(): Promise<TransactionResponse> {
  return await papaya.deposit(amount);
}
```
