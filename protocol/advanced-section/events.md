---
description: >-
  This section covers the core fund management functions for depositing and
  withdrawing tokens from the Papaya protocol.
---

# Deposit & Withdraw

### deposit

Deposits tokens into the user's account for streaming payments.

```solidity
function deposit(uint256 amount, bool isPermit2) external
```

#### Parameters

* `amount` (uint256): The amount of tokens to deposit
* `isPermit2` (bool): Whether to use Permit2 for the transfer

#### Description

This function allows users to deposit tokens into their Papaya account. The tokens are transferred from the caller's address to the contract. If `isPermit2` is true, the function uses the Permit2 protocol for the transfer.

#### Example

```javascript
// Deposit 1000 tokens using standard transfer
await papayaContract.deposit(ethers.utils.parseEther("1000"), false);

// Deposit using Permit2
await papayaContract.deposit(ethers.utils.parseEther("1000"), true);
```

### depositFor

Deposits tokens into a specific user's account.

```solidity
function depositFor(uint256 amount, address to, bool isPermit2) external
```

#### Parameters

* `amount` (uint256): The amount of tokens to deposit
* `to` (address): The address to deposit tokens for
* `isPermit2` (bool): Whether to use Permit2 for the transfer

#### Description

This function allows depositing tokens into another user's account. This is useful for applications that want to fund user accounts on their behalf.

#### Example

```javascript
// Deposit 500 tokens for another user
await papayaContract.depositFor(
  ethers.utils.parseEther("500"),
  "0x1234...",
  false
);
```

### withdraw

Withdraws tokens from the user's account.

```solidity
function withdraw(uint256 amount) external
```

#### Parameters

* `amount` (uint256): The amount of tokens to withdraw

#### Description

Allows users to withdraw their deposited tokens back to their address. The tokens are transferred from the contract to the caller's address.

#### Example

```javascript
// Withdraw 100 tokens
await papayaContract.withdraw(ethers.utils.parseEther("100"));
```

### withdrawTo

Withdraws tokens from the user's account to a specific address.

```solidity
function withdrawTo(address to, uint256 amount) external
```

#### Parameters

* `to` (address): The address to withdraw tokens to
* `amount` (uint256): The amount of tokens to withdraw

#### Description

Allows users to withdraw their deposited tokens to a specific address. This is useful for withdrawing to a different wallet or contract.

#### Example

```javascript
// Withdraw 200 tokens to another address
await papayaContract.withdrawTo(
  "0x5678...",
  ethers.utils.parseEther("200")
);
```

### pay

Pays tokens directly to a receiver.

```solidity
function pay(address receiver, uint256 amount) external
```

#### Parameters

* `receiver` (address): The address to pay tokens to
* `amount` (uint256): The amount of tokens to pay

#### Description

Allows users to pay tokens directly to a receiver without creating a subscription. This is useful for one-time payments.

#### Example

```javascript
// Pay 50 tokens to a receiver
await papayaContract.pay(
  "0x9abc...",
  ethers.utils.parseEther("50")
);
```

### rescueFunds

Rescues tokens that may be stuck in the contract.

```solidity
function rescueFunds(contract IERC20 token, uint256 amount) external
```

#### Parameters

* `token` (address): The token address to rescue
* `amount` (uint256): The amount of tokens to rescue

#### Description

Allows the contract owner to rescue tokens that may be stuck in the contract. This is an emergency function for recovering funds.

#### Example

```javascript
// Rescue 1000 tokens (owner only)
await papayaContract.rescueFunds(
  tokenAddress,
  ethers.utils.parseEther("1000")
);
```

### Related Events

* [Refill](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/core-events#refill): Emitted when funds are deposited
* [Transfer](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/core-events#transfer): Emitted when tokens are transferred

### Related Errors

* [InsufficientBalance](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#insufficientbalance): When trying to withdraw more than available balance
* [SafeTransferFailed](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#safetransferfailed): When token transfer fails
* [OwnableUnauthorizedAccount](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#ownableunauthorizedaccount): When non-owner tries to rescue funds
