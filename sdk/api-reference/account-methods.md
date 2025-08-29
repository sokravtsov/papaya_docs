---
description: Account methods of Papaya SDK for getting balance and user information
---

# Account Methods

### `balanceOf()`

Retrieves the token balance of an account in the Papaya protocol.

```typescript
async balanceOf(account?: string): Promise<number>
```

**Parameters:**

* `account`: (Optional) The address to check the balance of. If not provided, uses the connected signer's address.

**Returns:** The account balance in its raw blockchain format. Use `formatOutput()` to convert to a human-readable number.

**Example:**

```typescript
// Get raw balance
const rawBalance = await papaya.balanceOf();

// Convert to human-readable format
const balance = formatOutput(BigInt(rawBalance), 18);
console.log(`My balance: ${balance} USDT`);
```

### `getUserInfo()`

Gets detailed information about a user's account.

```typescript
async getUserInfo(account?: string): Promise<UserInfo>
```

**Parameters:**

* `account`: (Optional) The address to get info for. If not provided, uses the connected signer's address.

**Returns:** A `UserInfo` object with the following properties:

* `balance`: The account balance in raw blockchain format
* `incomeRate`: The rate at which the account is receiving subscriptions (raw format)
* `outgoingRate`: The rate at which the account is paying subscriptions (raw format)
* `updated`: The timestamp when the account was last updated

{% hint style="info" %}
The `incomeRate` and `outgoingRate` values are rates in their raw blockchain format. You should use the [utility functions](../utilities/) to convert them to human-readable values, typically per month.
{% endhint %}

**Example:**

```typescript
// Get raw user info
const userInfo = await papaya.getUserInfo();

// Convert to human-readable format
const formattedUserInfo = {
  balance: formatOutput(BigInt(userInfo.balance), 18),
  incomeRate: convertRateToPeriod(Number(formatOutput(userInfo.incomeRate, 18)), RatePeriod.MONTH),
  outgoingRate: convertRateToPeriod(Number(formatOutput(userInfo.outgoingRate, 18)), RatePeriod.MONTH),
  updated: new Date(Number(userInfo.updated) * 1000).toLocaleString()
};

console.log(`Balance: ${formattedUserInfo.balance} USDT`);
console.log(`Income rate: ${formattedUserInfo.incomeRate} USDT per month`);
console.log(`Outgoing rate: ${formattedUserInfo.outgoingRate} USDT per month`);
console.log(`Last updated: ${formattedUserInfo.updated}`);
```
