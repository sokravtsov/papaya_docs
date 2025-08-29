---
description: >-
  Subscription methods of Papaya SDK for managing subscriptions to content
  creators
---

# Subscription Methods

### `subscribe()`

Creates a new subscription to a creator.

```typescript
async subscribe(
  author: string, 
  amount: number | bigint,
  period: RatePeriod = RatePeriod.MONTH,
  projectId: number
): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `author`: The address of the creator to subscribe to
* `amount`: The amount of tokens for the subscription period
* `period`: (Optional) The subscription period (default: RatePeriod.MONTH)
* `projectId`: The project ID associated with the subscription

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
const creatorAddress = '0x...';
const tx = await papaya.subscribe(creatorAddress, 10, RatePeriod.MONTH, 0);
await tx.wait();
```

### `subscribeBySig()`

Creates a subscription transaction that can be signed off-chain and executed by anyone.

```typescript
async subscribeBySig(
  author: string, 
  amount: number | bigint,
  period: RatePeriod = RatePeriod.MONTH,
  projectId: number,
  deadline: number
): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `author`: The address of the creator to subscribe to
* `amount`: The amount of tokens for the subscription period
* `period`: (Optional) The subscription period (default: RatePeriod.MONTH)
* `projectId`: The project ID associated with the subscription
* `deadline`: Timestamp after which the transaction can't be executed

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
const creatorAddress = '0x...';
const deadline = Math.floor(Date.now() / 1000) + 3600; // 1 hour from now
const tx = await papaya.subscribeBySig(creatorAddress, 10, RatePeriod.MONTH, 0, deadline);
await tx.wait();
```

### `unsubscribe()`

Cancels a subscription to a creator.

```typescript
async unsubscribe(author: string): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `author`: The address of the creator to unsubscribe from

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
const creatorAddress = '0x...';
const tx = await papaya.unsubscribe(creatorAddress);
await tx.wait();
```

### `unsubscribeBySig()`

Creates an unsubscribe transaction that can be signed off-chain and executed by anyone.

```typescript
async unsubscribeBySig(author: string, deadline: number): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `author`: The address of the creator to unsubscribe from
* `deadline`: Timestamp after which the transaction can't be executed

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
const creatorAddress = '0x...';
const deadline = Math.floor(Date.now() / 1000) + 3600; // 1 hour from now
const tx = await papaya.unsubscribeBySig(creatorAddress, deadline);
await tx.wait();
```

### `getSubscriptions()`

Gets all subscriptions for an account.

```typescript
async getSubscriptions(account?: string): Promise<Subscription[]>
```

**Parameters:**

* `account`: (Optional) The address to get subscriptions for. If not provided, uses the connected signer's address.

**Returns:** Array of `Subscription` objects, each containing:

* `recipient`: The address receiving the subscription
* `incomeRate`: The rate at which the recipient is receiving tokens (raw format)
* `outgoingRate`: The rate at which the subscriber is paying tokens (raw format)
* `projectId`: The project ID associated with the subscription

{% hint style="info" %}
The `incomeRate` and `outgoingRate` values are per-second rates in their raw blockchain format. You should use the [utility functions](../utilities/) to convert them to human-readable values.
{% endhint %}

**Example:**

```typescript
// Get raw subscriptions
const subscriptions = await papaya.getSubscriptions();

// Format the subscription rates to human-readable monthly values
const formattedSubscriptions = subscriptions.map(sub => ({
  recipient: sub.recipient,
  incomeRate: convertRateToPeriod(formatOutput(sub.incomeRate, 18), RatePeriod.MONTH),
  outgoingRate: convertRateToPeriod(formatOutput(sub.outgoingRate, 18), RatePeriod.MONTH),
  projectId: sub.projectId
}));
```
