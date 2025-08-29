---
description: >-
  This section covers the view functions for querying system-wide information
  and constants.
---

# System Information

### owner

Gets the contract owner address.

```solidity
function owner() external view returns (address)
```

#### Returns

* `owner` (address): The contract owner's address

#### Description

Returns the address of the contract owner who has administrative privileges.

#### Example

```javascript
// Get contract owner
const owner = await papayaContract.owner();
console.log("Contract owner:", owner);
```

### TOKEN

Gets the token address used by the contract.

```solidity
function TOKEN() external view returns (contract IERC20)
```

#### Returns

* `token` (address): The ERC20 token address

#### Description

Returns the address of the ERC20 token used by the Papaya protocol.

#### Example

```javascript
// Get token address
const tokenAddress = await papayaContract.TOKEN();
console.log("Token address:", tokenAddress);
```

### TOKEN\_PRICE\_FEED

Gets the token price feed address.

```solidity
function TOKEN_PRICE_FEED() external view returns (contract AggregatorV3Interface)
```

#### Returns

* `priceFeed` (address): The token price feed address

#### Description

Returns the address of the Chainlink price feed for the token.

#### Example

```javascript
// Get token price feed
const priceFeed = await papayaContract.TOKEN_PRICE_FEED();
console.log("Token price feed:", priceFeed);
```

### COIN\_PRICE\_FEED

Gets the native coin price feed address.

```solidity
function COIN_PRICE_FEED() external view returns (contract AggregatorV3Interface)
```

#### Returns

* `priceFeed` (address): The native coin price feed address

#### Description

Returns the address of the Chainlink price feed for the native coin (ETH).

#### Example

```javascript
// Get native coin price feed
const priceFeed = await papayaContract.COIN_PRICE_FEED();
console.log("Native coin price feed:", priceFeed);
```

### MAX\_PROTOCOL\_FEE

Gets the maximum protocol fee.

```solidity
function MAX_PROTOCOL_FEE() external view returns (uint256)
```

#### Returns

* `maxFee` (uint256): The maximum protocol fee

#### Description

Returns the maximum protocol fee that can be set.

#### Example

```javascript
// Get max protocol fee
const maxFee = await papayaContract.MAX_PROTOCOL_FEE();
console.log("Max protocol fee:", maxFee.toString());
```

### REFILL\_DAYS

Gets the refill days constant.

```solidity
function REFILL_DAYS() external view returns (uint32)
```

#### Returns

* `refillDays` (uint32): The refill days value

#### Description

Returns the number of days for refill operations.

#### Example

```javascript
// Get refill days
const refillDays = await papayaContract.REFILL_DAYS();
console.log("Refill days:", refillDays.toString());
```

### REFILL\_GAS\_COST

Gets the refill gas cost constant.

```solidity
function REFILL_GAS_COST() external view returns (uint32)
```

#### Returns

* `gasCost` (uint32): The refill gas cost

#### Description

Returns the gas cost for refill operations.

#### Example

```javascript
// Get refill gas cost
const gasCost = await papayaContract.REFILL_GAS_COST();
console.log("Refill gas cost:", gasCost.toString());
```

### APPROX\_LIQUIDATE\_GAS

Gets the approximate gas cost for liquidation.

```solidity
function APPROX_LIQUIDATE_GAS() external view returns (uint256)
```

#### Returns

* `gasCost` (uint256): The approximate liquidation gas cost

#### Description

Returns the approximate gas cost for liquidation operations.

#### Example

```javascript
// Get liquidation gas cost
const gasCost = await papayaContract.APPROX_LIQUIDATE_GAS();
console.log("Liquidation gas cost:", gasCost.toString());
```

### APPROX\_SUBSCRIPTION\_GAS

Gets the approximate gas cost for subscription operations.

```solidity
function APPROX_SUBSCRIPTION_GAS() external view returns (uint256)
```

#### Returns

* `gasCost` (uint256): The approximate subscription gas cost

#### Description

Returns the approximate gas cost for subscription operations.

#### Example

```javascript
// Get subscription gas cost
const gasCost = await papayaContract.APPROX_SUBSCRIPTION_GAS();
console.log("Subscription gas cost:", gasCost.toString());
```

### SUBSCRIPTION\_THRESHOLD

Gets the subscription threshold.

```solidity
function SUBSCRIPTION_THRESHOLD() external view returns (uint8)
```

#### Returns

* `threshold` (uint8): The subscription threshold

#### Description

Returns the threshold value for subscription operations.

#### Example

```javascript
// Get subscription threshold
const threshold = await papayaContract.SUBSCRIPTION_THRESHOLD();
console.log("Subscription threshold:", threshold.toString());
```

### DECIMALS\_SCALE

Gets the decimals scale constant.

```solidity
function DECIMALS_SCALE() external view returns (uint256)
```

#### Returns

* `scale` (uint256): The decimals scale

#### Description

Returns the scale factor used for decimal calculations.

#### Example

```javascript
// Get decimals scale
const scale = await papayaContract.DECIMALS_SCALE();
console.log("Decimals scale:", scale.toString());
```

### FLOOR

Gets the floor value constant.

```solidity
function FLOOR() external view returns (uint256)
```

#### Returns

* `floor` (uint256): The floor value

#### Description

Returns the floor value used in calculations.

#### Example

```javascript
// Get floor value
const floor = await papayaContract.FLOOR();
console.log("Floor value:", floor.toString());
```

### SIGNED\_CALL\_TYPEHASH

Gets the signed call typehash.

```solidity
function SIGNED_CALL_TYPEHASH() external view returns (bytes32)
```

#### Returns

* `typehash` (bytes32): The signed call typehash

#### Description

Returns the typehash used for EIP-712 signed calls.

#### Example

```javascript
// Get signed call typehash
const typehash = await papayaContract.SIGNED_CALL_TYPEHASH();
console.log("Signed call typehash:", typehash);
```

### eip712Domain

Gets the EIP-712 domain information.

```solidity
function eip712Domain() external view returns (bytes1 fields, string memory name, string memory version, uint256 chainId, address verifyingContract, bytes32 salt, uint256[] memory extensions)
```

#### Returns

* `fields` (bytes1): The domain fields
* `name` (string): The domain name
* `version` (string): The domain version
* `chainId` (uint256): The chain ID
* `verifyingContract` (address): The verifying contract address
* `salt` (bytes32): The domain salt
* `extensions` (uint256\[]): The domain extensions

#### Description

Returns the EIP-712 domain information used for signature verification.

#### Example

```javascript
// Get EIP-712 domain
const domain = await papayaContract.eip712Domain();
console.log("Domain name:", domain.name);
console.log("Domain version:", domain.version);
console.log("Chain ID:", domain.chainId.toString());
console.log("Verifying contract:", domain.verifyingContract);
```
