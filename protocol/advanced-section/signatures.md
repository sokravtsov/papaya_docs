---
description: This section covers the liquidation functionality for underfunded accounts.
---

# Liquidation

### liquidate

Liquidates an underfunded account.

```solidity
function liquidate(address account) external
```

#### Parameters

* `account` (address): The address of the account to liquidate

#### Description

Allows anyone to liquidate an account that has insufficient funds to cover its streaming obligations. The liquidator receives a reward for performing the liquidation.

#### Example

```javascript
// Liquidate an underfunded account
await papayaContract.liquidate("0xunderfunded...");
```

### Related Events

* [Liquidated](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/core-events#liquidated): Emitted when an account is liquidated

### Related Errors

* [NotLiquidatable](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#notliquidatable): When the account cannot be liquidated
* [InsufficientBalance](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#insufficientbalance): When the account has insufficient balance for liquidation
