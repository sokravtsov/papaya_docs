---
description: >-
  This section covers the core payment and streaming functionality of the Papaya
  protocol.
---

# Payment & Streaming

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

### Related Events

* [Transfer](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/core-events#transfer): Emitted when tokens are transferred during streaming

### Related Errors

* [WrongSignature](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#wrongsignature): When permit signature is invalid
* [DeadlineExceeded](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#deadlineexceeded): When permit has expired

