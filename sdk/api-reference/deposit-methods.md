---
description: Deposit methods of Papaya SDK for depositing tokens into the protocol
---

# Deposit Methods

### `deposit()`

Deposits tokens into the Papaya protocol.

```typescript
async deposit(amount: bigint | number, isPermit2: boolean = false): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `amount`: The amount of tokens to deposit, should be formatted using `formatInput()`
* `isPermit2`: (Optional) Whether to use Permit2 for the deposit (default: false)

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
// Format the amount correctly (10 USDT with 6 decimals)
const amount = formatInput('10', 6);

// Deposit
const tx = await papaya.deposit(amount);
await tx.wait();
console.log('Deposit successful');
```

### `depositBySig()`

Creates a deposit transaction that can be signed off-chain and executed by anyone.

```typescript
async depositBySig(amount: bigint | number, deadline: number): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `amount`: The amount of tokens to deposit, should be formatted using `formatInput()`
* `deadline`: Timestamp after which the transaction can't be executed

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
// Format the amount correctly (10 USDT with 6 decimals)
const amount = formatInput('10', 6);

// Set deadline to 1 hour from now
const deadline = Math.floor(Date.now() / 1000) + 3600;

// Create the depositBySig transaction
const tx = await papaya.depositBySig(amount, deadline);
await tx.wait();
```

### `depositFor()`

Deposits tokens into another account.

```typescript
async depositFor(amount: bigint | number, to: string, isPermit2: boolean = false): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `amount`: The amount of tokens to deposit, should be formatted using `formatInput()`
* `to`: The recipient address
* `isPermit2`: (Optional) Whether to use Permit2 for the deposit (default: false)

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
// Format the amount correctly (50 USDT with 6 decimals)
const amount = formatInput('50', 6);
const recipientAddress = '0x...';

// Deposit to the recipient
const tx = await papaya.depositFor(amount, recipientAddress);
await tx.wait();
```
