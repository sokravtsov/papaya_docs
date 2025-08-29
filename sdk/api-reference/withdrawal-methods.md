---
description: Withdrawal methods of Papaya SDK for withdrawing tokens from the protocol
---

# Withdrawal Methods

### `withdraw()`

Withdraws tokens from the Papaya protocol.

```typescript
async withdraw(amount: bigint | number): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `amount`: The amount of tokens to withdraw, should be formatted using `formatInput()`

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
// Format the amount correctly (50 USDT with 18 decimals)
const amount = formatInput('50', 18);

// Withdraw
const tx = await papaya.withdraw(amount);
await tx.wait();
console.log('Withdrawal successful');
```

### `withdrawBySig()`

Creates a withdrawal transaction that can be signed off-chain and executed by anyone.

```typescript
async withdrawBySig(amount: bigint | number, deadline: number): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `amount`: The amount of tokens to withdraw, should be formatted using `formatInput()`
* `deadline`: Timestamp after which the transaction can't be executed

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
// Format the amount correctly (50 USDT with 18 decimals)
const amount = formatInput('50', 18);

// Set deadline to 1 hour from now
const deadline = Math.floor(Date.now() / 1000) + 3600;

// Create the withdrawBySig transaction
const tx = await papaya.withdrawBySig(amount, deadline);
await tx.wait();
```

### `withdrawTo()`

Withdraws tokens directly to another address.

```typescript
async withdrawTo(to: string, amount: bigint | number): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `to`: The recipient address
* `amount`: The amount of tokens to withdraw, should be formatted using `formatInput()`

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
const recipientAddress = '0x...';
// Format the amount correctly (25 USDT with 18 decimals)
const amount = formatInput('25', 18);

// Withdraw to the recipient
const tx = await papaya.withdrawTo(recipientAddress, amount);
await tx.wait();
```
