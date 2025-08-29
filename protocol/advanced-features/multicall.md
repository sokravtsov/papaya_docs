---
description: >-
  This section covers the multicall functionality for executing multiple
  operations in a single transaction.
---

# Multicall

### multicall

Executes multiple calls in a single transaction.

```solidity
function multicall(bytes[] data) external returns (bytes[] memory results)
```

#### Parameters

* `data` (bytes\[]): Array of encoded function calls

#### Description

Executes multiple function calls in a single transaction. This is useful for batching operations to save gas and ensure atomicity.

#### Example

```javascript
// Execute multiple calls in one transaction
const calls = [
  papayaContract.interface.encodeFunctionData("deposit", [ethers.utils.parseEther("100"), false]),
  papayaContract.interface.encodeFunctionData("subscribe", ["0xauthor...", ethers.utils.parseEther("0.001"), 1])
];

const results = await papayaContract.multicall(calls);
```

### Related Errors

* [FailedCall](broken-reference): When any of the multicall operations fail
