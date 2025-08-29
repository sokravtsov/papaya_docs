---
description: This section covers the core events emitted by the Papaya protocol.
---

# Core Events

### Transfer

Emitted when tokens are transferred.

```solidity
event Transfer(address indexed _from, address indexed _to, uint256 _value)
```

#### Parameters

* `_from` (address, indexed): The address tokens are transferred from
* `_to` (address, indexed): The address tokens are transferred to
* `_value` (uint256): The amount of tokens transferred

#### Description

Standard ERC20 transfer event emitted when tokens are moved between addresses.

#### Example

```javascript
// Listen for transfer events
papayaContract.on("Transfer", (from, to, value) => {
  console.log(`Transfer: ${value} tokens from ${from} to ${to}`);
});
```

### Refill

Emitted when funds are deposited into an account.

```solidity
event Refill(address indexed user, uint256 amount)
```

#### Parameters

* `user` (address, indexed): The user who received the funds
* `amount` (uint256): The amount of tokens deposited

#### Description

Emitted when tokens are deposited into a user's account through the `deposit` or `depositFor` functions.

#### Example

```javascript
// Listen for refill events
papayaContract.on("Refill", (user, amount) => {
  console.log(`Refill: ${amount} tokens deposited for ${user}`);
});
```

### Liquidated

Emitted when an account is liquidated.

```solidity
event Liquidated(address indexed user, address indexed liquidator)
```

#### Parameters

* `user` (address, indexed): The address of the liquidated user
* `liquidator` (address, indexed): The address of the liquidator

#### Description

Emitted when an underfunded account is liquidated by the `liquidate` function.

#### Example

```javascript
// Listen for liquidation events
papayaContract.on("Liquidated", (user, liquidator) => {
  console.log(`Liquidated: ${user} was liquidated by ${liquidator}`);
});
```

### OwnershipTransferred

Emitted when contract ownership is transferred.

```solidity
event OwnershipTransferred(address indexed previousOwner, address indexed newOwner)
```

#### Parameters

* `previousOwner` (address, indexed): The previous owner's address
* `newOwner` (address, indexed): The new owner's address

#### Description

Emitted when the contract ownership is transferred to a new address.

#### Example

```javascript
// Listen for ownership transfer events
papayaContract.on("OwnershipTransferred", (previousOwner, newOwner) => {
  console.log(`Ownership transferred from ${previousOwner} to ${newOwner}`);
});
```

### EIP712DomainChanged

Emitted when the EIP-712 domain is changed.

```solidity
event EIP712DomainChanged()
```

#### Description

Emitted when the EIP-712 domain information is updated.

#### Example

```javascript
// Listen for EIP-712 domain change events
papayaContract.on("EIP712DomainChanged", () => {
  console.log("EIP-712 domain changed");
});
```
