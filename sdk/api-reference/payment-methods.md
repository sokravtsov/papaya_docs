---
description: Methods for making one-time payments in the Papaya protocol
---

# Payment Methods

### `pay()`

Makes a one-time payment to a recipient.

```typescript
async pay(receiver: string, amount: bigint | number): Promise<ethers.TransactionResponse>
```

**Parameters:**

* `receiver`: The recipient's address
* `amount`: The amount of tokens to pay, should be formatted using `formatInput()`

**Returns:** An ethers.js `TransactionResponse` object.

**Example:**

```typescript
const recipientAddress = '0x...';
// Format the amount correctly (20 USDT with 6 decimals)
const amount = formatInput('20', 6);

// Make the payment
const tx = await papaya.pay(recipientAddress, amount);
await tx.wait();
```
