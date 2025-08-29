---
description: >-
  Formatting functions of Papaya SDK for working with numbers and blockchain
  data
---

# Formatting Functions

{% hint style="info" %}
The SDK provides functions for formatting amounts between different representations.
{% endhint %}

### `formatInput()`

Converts a human-readable amount into a bigint for use in blockchain transactions.

```typescript
function formatInput(amount: string, unit?: string | ethers.Numeric): bigint
```

**Parameters:**

* `amount`: The amount as a string
* `unit`: (Optional) The unit of the amount (e.g., "18" for 18 decimal places)

**Returns:** The formatted bigint amount.

**Example:**

```typescript
// Format 10 USDT for transaction (USDT has 6 decimal places)
const amount = formatInput('10', 6);
console.log(amount); // 10000000n

// Format 1.5 ETH for transaction (ETH has 18 decimal places)
const ethAmount = formatInput('1.5', 18);
console.log(ethAmount); // 1500000000000000000n
```

### `formatOutput()`

Converts a bigint amount from blockchain to a human-readable number.

```typescript
function formatOutput(amount: bigint | number, unit?: string | ethers.Numeric): string
```

**Parameters:**

* `amount`: The amount as bigint or number
* `unit`: (Optional) The unit of the amount (e.g., "18" for 18 decimal places)

**Returns:** The formatted amount as a string.

**Example:**

```typescript
// Convert raw USDT balance to readable format
const rawBalance = 10000000n; // 10 USDT in raw format
const readableBalance = formatOutput(rawBalance, 6);
console.log(readableBalance); // "10.0"

// Convert raw ETH balance to readable format
const rawEthBalance = 1500000000000000000n; // 1.5 ETH in raw format
const readableEthBalance = formatOutput(rawEthBalance, 18);
console.log(readableEthBalance); // "1.5"
```

### Practical Examples

#### Working with Balances

```typescript
import { formatInput, formatOutput } from '@papaya_fi/sdk';

// Get user balance
const rawBalance = await papaya.balanceOf();

// Convert to human-readable format for display
const displayBalance = formatOutput(BigInt(rawBalance), 18);
console.log(`Your balance: ${displayBalance} USDT`);

// User wants to withdraw 25 USDT
const withdrawalAmount = formatInput('25', 18);
const tx = await papaya.withdraw(withdrawalAmount);
await tx.wait();
```

#### Working with Different Tokens

```typescript
// USDT has 6 decimal places
const usdtAmount = formatInput('100', 6); // 100000000n

// USDC also has 6 decimal places
const usdcAmount = formatInput('50', 6); // 50000000n

// ETH has 18 decimal places
const ethAmount = formatInput('0.1', 18); // 100000000000000000n
```

#### Error Handling

```typescript
try {
  const amount = formatInput('invalid', 18);
} catch (error) {
  console.error('Formatting error:', error.message);
  // Error: invalid value for BigInt
}

try {
  const amount = formatInput('-10', 18);
} catch (error) {
  console.error('Formatting error:', error.message);
  // Error: negative value for BigInt
}
```
