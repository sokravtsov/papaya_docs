---
description: >-
  This section covers the BySig functionality for gasless operations using
  signatures.
---

# BySig Operations

### bySig

Executes a signed call with a signature.

```solidity
function bySig(address signer, BySig.SignedCall memory sig, bytes signature) external payable returns (bytes memory ret)
```

#### Parameters

* `signer` (address): The address that signed the call
* `sig` (BySig.SignedCall): The signed call data containing:
  * `traits` (uint256): The BySig traits
  * `data` (bytes): The call data
* `signature` (bytes): The signature for the call

#### Description

Executes a call that was signed off-chain. This allows for gasless interactions where users sign messages off-chain and others can execute them on-chain.

#### Example

```javascript
// Execute a signed call
const result = await papayaContract.bySig(
  signerAddress,
  signedCallData,
  signature,
  { value: ethers.utils.parseEther("0.1") }
);
```

### hashBySig

Computes the hash of a BySig call.

```solidity
function hashBySig(BySig.SignedCall memory sig) external view returns (bytes32)
```

#### Parameters

* `sig` (BySig.SignedCall): The signed call data

#### Description

Computes the hash of a BySig call for signature verification.

#### Example

```javascript
// Hash a BySig call
const hash = await papayaContract.hashBySig(signedCallData);
```

### useBySigAccountNonce

Advances the account nonce for BySig operations.

```solidity
function useBySigAccountNonce(uint32 advance) external
```

#### Parameters

* `advance` (uint32): The number of nonces to advance

#### Description

Advances the account nonce used for BySig operations. This is useful for invalidating old signatures.

#### Example

```javascript
// Advance account nonce by 1
await papayaContract.useBySigAccountNonce(1);
```

### useBySigSelectorNonce

Advances the selector nonce for BySig operations.

```solidity
function useBySigSelectorNonce(bytes4 selector, uint32 advance) external
```

#### Parameters

* `selector` (bytes4): The function selector
* `advance` (uint32): The number of nonces to advance

#### Description

Advances the selector-specific nonce used for BySig operations.

#### Example

```javascript
// Advance selector nonce by 1
await papayaContract.useBySigSelectorNonce("0x12345678", 1);
```

### useBySigUniqueNonce

Uses a unique nonce for BySig operations.

```solidity
function useBySigUniqueNonce(uint256 nonce) external
```

#### Parameters

* `nonce` (uint256): The unique nonce to use

#### Description

Uses a specific unique nonce for BySig operations. This allows for precise control over signature replay protection.

#### Example

```javascript
// Use a specific unique nonce
await papayaContract.useBySigUniqueNonce(12345);
```

### Related Errors

* [WrongSignature](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#wrongsignature): When signature is invalid
* [WrongNonce](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#wrongnonce): When nonce is incorrect
* [WrongNonceType](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#wrongnoncetype): When nonce type is invalid
