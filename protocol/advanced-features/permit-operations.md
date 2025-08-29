---
description: This section covers the permit functionality for gasless token approvals.
---

# Permit Operations

### permitAndCall

Executes a permit and then performs an action in a single transaction.

```solidity
function permitAndCall(bytes permit, bytes action) external payable
```

#### Parameters

* `permit` (bytes): The permit data for token approval
* `action` (bytes): The action to execute after the permit

#### Description

This function allows users to approve tokens and execute an action in a single transaction. This is useful for gasless interactions where users sign permits off-chain.

#### Example

```javascript
// Execute permit and action in one transaction
await papayaContract.permitAndCall(permitData, actionData, {
  value: ethers.utils.parseEther("0.1")
});
```

### Related Errors

* [WrongSignature](broken-reference): When permit signature is invalid
* [DeadlineExceeded](broken-reference): When permit has expired
* [Permit2TransferAmountTooHigh](broken-reference): When permit2 transfer amount is too high
