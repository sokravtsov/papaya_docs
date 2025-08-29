---
description: >-
  This section covers all the error codes that can be thrown by the Papaya
  protocol.
---

# Error Codes

### AccessDenied

Thrown when access is denied for a specific project.

```solidity
error AccessDenied(uint256 projectId)
```

#### Parameters

* `projectId` (uint256): The project ID for which access was denied

#### Description

Thrown when a caller doesn't have permission to perform an action on a specific project.

### AddressEmptyCode

Thrown when trying to call a contract with empty code.

```solidity
error AddressEmptyCode(address target)
```

#### Parameters

* `target` (address): The target address with empty code

#### Description

Thrown when attempting to call a contract that has no code at the target address.

### DeadlineExceeded

Thrown when a deadline has been exceeded.

```solidity
error DeadlineExceeded()
```

#### Description

Thrown when a permit or other time-sensitive operation has exceeded its deadline.

### EnumerableMapNonexistentKey

Thrown when trying to access a non-existent key in an enumerable map.

```solidity
error EnumerableMapNonexistentKey(bytes32 key)
```

#### Parameters

* `key` (bytes32): The non-existent key

#### Description

Thrown when attempting to access a key that doesn't exist in an enumerable map.

### ExcessOfRate

Thrown when the subscription rate exceeds the maximum allowed rate.

```solidity
error ExcessOfRate()
```

#### Description

Thrown when trying to create a subscription with a rate that exceeds the protocol limits.

### ExcessOfSubscriptions

Thrown when a user has too many active subscriptions.

```solidity
error ExcessOfSubscriptions()
```

#### Description

Thrown when trying to create a subscription but the user has already reached the maximum number of active subscriptions.

### FailedCall

Thrown when a call to another contract fails.

```solidity
error FailedCall()
```

#### Description

Thrown when a call to an external contract fails.

### IndexOutOfBounds

Thrown when trying to access an index that is out of bounds.

```solidity
error IndexOutOfBounds()
```

#### Description

Thrown when attempting to access an array index that doesn't exist.

### InsufficientBalance

Thrown when there are insufficient funds for an operation.

```solidity
error InsufficientBalance(uint256 balance, uint256 needed)
```

#### Parameters

* `balance` (uint256): The current balance
* `needed` (uint256): The amount needed

#### Description

Thrown when trying to perform an operation that requires more funds than are available.

### InsufficialBalance

Thrown when there are insufficient official funds.

```solidity
error InsufficialBalance()
```

#### Description

Thrown when there are insufficient official funds for an operation.

### InvalidProjectId

Thrown when an invalid project ID is provided.

```solidity
error InvalidProjectId(uint256 projectId)
```

#### Parameters

* `projectId` (uint256): The invalid project ID

#### Description

Thrown when trying to use a project ID that doesn't exist or is invalid.

### InvalidShortString

Thrown when a short string is invalid.

```solidity
error InvalidShortString()
```

#### Description

Thrown when a short string doesn't meet the required format.

### NotLegal

Thrown when an operation is not legal.

```solidity
error NotLegal()
```

#### Description

Thrown when an operation violates legal or protocol rules.

### NotLiquidatable

Thrown when an account cannot be liquidated.

```solidity
error NotLiquidatable()
```

#### Description

Thrown when trying to liquidate an account that doesn't meet the liquidation criteria.

### NotSubscribed

Thrown when trying to perform an operation on a non-existent subscription.

```solidity
error NotSubscribed()
```

#### Description

Thrown when trying to unsubscribe from a subscription that doesn't exist.

### OwnableInvalidOwner

Thrown when an invalid owner address is provided.

```solidity
error OwnableInvalidOwner(address owner)
```

#### Parameters

* `owner` (address): The invalid owner address

#### Description

Thrown when trying to set an invalid address as the contract owner.

### OwnableUnauthorizedAccount

Thrown when an unauthorized account tries to perform an owner-only operation.

```solidity
error OwnableUnauthorizedAccount(address account)
```

#### Parameters

* `account` (address): The unauthorized account

#### Description

Thrown when an account without owner privileges tries to perform an owner-only operation.

### Permit2TransferAmountTooHigh

Thrown when the Permit2 transfer amount is too high.

```solidity
error Permit2TransferAmountTooHigh()
```

#### Description

Thrown when trying to transfer more tokens than allowed through Permit2.

### ReduceTheAmount

Thrown when the amount needs to be reduced.

```solidity
error ReduceTheAmount()
```

#### Description

Thrown when the requested amount is too high and needs to be reduced.

### SafeCastOverflowedUintToInt

Thrown when a safe cast from uint to int overflows.

```solidity
error SafeCastOverflowedUintToInt(uint256 value)
```

#### Parameters

* `value` (uint256): The value that caused the overflow

#### Description

Thrown when trying to cast a uint256 to int256 that would cause an overflow.

### SafeTransferFailed

Thrown when a safe transfer operation fails.

```solidity
error SafeTransferFailed()
```

#### Description

Thrown when a safe transfer of tokens fails.

### SafeTransferFromFailed

Thrown when a safe transfer from operation fails.

```solidity
error SafeTransferFromFailed()
```

#### Description

Thrown when a safe transfer from operation fails.

### StringTooLong

Thrown when a string is too long.

```solidity
error StringTooLong(string str)
```

#### Parameters

* `str` (string): The string that is too long

#### Description

Thrown when a string exceeds the maximum allowed length.

### TopUpBalance

Thrown when the balance needs to be topped up.

```solidity
error TopUpBalance()
```

#### Description

Thrown when the account balance is insufficient and needs to be topped up.

### WrongNonce

Thrown when an incorrect nonce is provided.

```solidity
error WrongNonce()
```

#### Description

Thrown when a nonce doesn't match the expected value for BySig operations.

### WrongNonceType

Thrown when an incorrect nonce type is provided.

```solidity
error WrongNonceType()
```

#### Description

Thrown when the nonce type doesn't match the expected type for BySig operations.

### WrongPercent

Thrown when an incorrect percentage is provided.

```solidity
error WrongPercent()
```

#### Description

Thrown when a percentage value is outside the allowed range.

### WrongRelayer

Thrown when an incorrect relayer is provided.

```solidity
error WrongRelayer()
```

#### Description

Thrown when the relayer address doesn't match the expected value.

### WrongSignature

Thrown when a signature is invalid.

```solidity
error WrongSignature()
```

#### Description

Thrown when a signature doesn't match the expected value or is invalid.

### WrongToken

Thrown when an incorrect token is provided.

```solidity
error WrongToken()
```

#### Description

Thrown when trying to use a token that is not supported by the protocol.
