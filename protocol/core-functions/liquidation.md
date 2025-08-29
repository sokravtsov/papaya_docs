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

* [Liquidated](broken-reference): Emitted when an account is liquidated

### Related Errors

* [NotLiquidatable](broken-reference): When the account cannot be liquidated
* [InsufficientBalance](broken-reference): When the account has insufficient balance for liquidation
