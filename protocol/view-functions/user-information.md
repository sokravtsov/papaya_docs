---
description: This section covers the view functions for querying user account information.
---

# User Information

### users

Gets detailed information about a user's account.

```solidity
function users(address account) external view returns (int256 balance, int256 incomeRate, int256 outgoingRate, uint256 updated)
```

#### Parameters

* `account` (address): The user's address

#### Returns

* `balance` (int256): The user's current balance
* `incomeRate` (int256): The rate at which tokens are flowing into the account
* `outgoingRate` (int256): The rate at which tokens are flowing out of the account
* `updated` (uint256): The timestamp of the last update

#### Description

Returns comprehensive information about a user's account including their balance and streaming rates.

#### Example

```javascript
// Get user information
const userInfo = await papayaContract.users("0xuser...");
console.log("Balance:", userInfo.balance.toString());
console.log("Income Rate:", userInfo.incomeRate.toString());
console.log("Outgoing Rate:", userInfo.outgoingRate.toString());
console.log("Last Updated:", userInfo.updated.toString());
```

### balanceOf

Gets the balance of a specific account.

```solidity
function balanceOf(address account) external view returns (uint256)
```

#### Parameters

* `account` (address): The account address

#### Returns

* `balance` (uint256): The account balance

#### Description

Returns the current balance of the specified account.

#### Example

```javascript
// Get account balance
const balance = await papayaContract.balanceOf("0xuser...");
console.log("Balance:", ethers.utils.formatEther(balance));
```

### bySigAccountNonces

Gets the account nonce for BySig operations.

```solidity
function bySigAccountNonces(address account) external view returns (uint256)
```

#### Parameters

* `account` (address): The account address

#### Returns

* `nonce` (uint256): The current account nonce

#### Description

Returns the current nonce for BySig operations for a specific account.

#### Example

```javascript
// Get account nonce
const nonce = await papayaContract.bySigAccountNonces("0xuser...");
console.log("Account nonce:", nonce.toString());
```

### bySigSelectorNonces

Gets the selector nonce for BySig operations.

```solidity
function bySigSelectorNonces(address account, bytes4 selector) external view returns (uint256)
```

#### Parameters

* `account` (address): The account address
* `selector` (bytes4): The function selector

#### Returns

* `nonce` (uint256): The current selector nonce

#### Description

Returns the current nonce for a specific function selector in BySig operations.

#### Example

```javascript
// Get selector nonce
const nonce = await papayaContract.bySigSelectorNonces("0xuser...", "0x12345678");
console.log("Selector nonce:", nonce.toString());
```

### bySigUniqueNonces

Checks if a unique nonce has been used.

```solidity
function bySigUniqueNonces(address account, uint256 nonce) external view returns (bool)
```

#### Parameters

* `account` (address): The account address
* `nonce` (uint256): The unique nonce to check

#### Returns

* `used` (bool): Whether the nonce has been used

#### Description

Returns whether a specific unique nonce has been used for BySig operations.

#### Example

```javascript
// Check if nonce is used
const used = await papayaContract.bySigUniqueNonces("0xuser...", 12345);
console.log("Nonce used:", used);
```

### bySigUniqueNoncesSlot

Gets the storage slot for a unique nonce.

```solidity
function bySigUniqueNoncesSlot(address account, uint256 nonce) external view returns (uint256)
```

#### Parameters

* `account` (address): The account address
* `nonce` (uint256): The unique nonce

#### Returns

* `slot` (uint256): The storage slot for the nonce

#### Description

Returns the storage slot used for tracking a specific unique nonce.

#### Example

```javascript
// Get nonce storage slot
const slot = await papayaContract.bySigUniqueNoncesSlot("0xuser...", 12345);
console.log("Nonce slot:", slot.toString());
```

### name

Gets the name of the token.

```solidity
function name() external pure returns (string memory)
```

#### Returns

* `name` (string): The token name

#### Description

Returns the name of the Papaya token.

#### Example

```javascript
// Get token name
const name = await papayaContract.name();
console.log("Token Name:", name);
```

### symbol

Gets the symbol of the token.

```solidity
function symbol() external pure returns (string memory)
```

#### Returns

* `symbol` (string): The token symbol

#### Description

Returns the symbol of the Papaya token.

#### Example

```javascript
// Get token symbol
const symbol = await papayaContract.symbol();
console.log("Token Symbol:", symbol);
```

### decimals

Gets the number of decimals for the token.

```solidity
function decimals() external pure returns (uint8)
```

#### Returns

* `decimals` (uint8): The number of decimals

#### Description

Returns the number of decimals used by the token.

#### Example

```javascript
// Get token decimals
const decimals = await papayaContract.decimals();
console.log("Decimals:", decimals);
```

### totalSupply

Gets the total supply of tokens.

```solidity
function totalSupply() external view returns (uint256)
```

#### Returns

* `totalSupply` (uint256): The total token supply

#### Description

Returns the total supply of Papaya tokens.

#### Example

```javascript
// Get total supply
const totalSupply = await papayaContract.totalSupply();
console.log("Total Supply:", ethers.utils.formatEther(totalSupply));
```
