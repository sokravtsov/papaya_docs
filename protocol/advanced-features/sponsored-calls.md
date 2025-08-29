---
description: This section covers the sponsored call functionality for gasless transactions.
---

# Sponsored Calls

### sponsoredCall

Executes a sponsored call with token payment.

```solidity
function sponsoredCall(address token, uint256 amount, bytes data, bytes extraData) external payable returns (bytes memory ret)
```

#### Parameters

* `token` (address): The token address for payment
* `amount` (uint256): The amount of tokens to pay
* `data` (bytes): The call data to execute
* `extraData` (bytes): Additional data for the call

#### Description

Executes a call that is sponsored by the caller. The caller pays for the gas and can optionally pay tokens as part of the transaction.

#### Example

```javascript
// Execute a sponsored call
const result = await papayaContract.sponsoredCall(
  tokenAddress,
  ethers.utils.parseEther("10"),
  callData,
  extraData,
  { value: ethers.utils.parseEther("0.1") }
);
```

### Related Errors

* [FailedCall](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#failedcall): When the sponsored call fails
* [SafeTransferFailed](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#safetransferfailed): When token transfer fails
