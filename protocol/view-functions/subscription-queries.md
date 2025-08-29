---
description: This section covers the view functions for querying subscription information.
---

# Subscription Queries

### subscriptions

Gets subscription information between two addresses.

```solidity
function subscriptions(address from, address to) external view returns (bool, uint256 encodedRates)
```

#### Parameters

* `from` (address): The subscriber's address
* `to` (address): The author's address

#### Returns

* `exists` (bool): Whether the subscription exists
* `encodedRates` (uint256): The encoded subscription rates

#### Description

Returns information about a subscription between two addresses, including whether it exists and the encoded rates.

#### Example

```javascript
// Get subscription information
const [exists, encodedRates] = await papayaContract.subscriptions("0xsubscriber...", "0xauthor...");
console.log("Subscription exists:", exists);
console.log("Encoded rates:", encodedRates.toString());
```

### allSubscriptions

Gets all subscriptions for a specific address.

```solidity
function allSubscriptions(address from) external view returns (address[] to, uint256[] encodedRates)
```

#### Parameters

* `from` (address): The subscriber's address

#### Returns

* `to` (address\[]): Array of author addresses
* `encodedRates` (uint256\[]): Array of encoded subscription rates

#### Description

Returns all active subscriptions for a specific subscriber address.

#### Example

```javascript
// Get all subscriptions for a user
const [authors, rates] = await papayaContract.allSubscriptions("0xsubscriber...");
console.log("Number of subscriptions:", authors.length);
for (let i = 0; i < authors.length; i++) {
  console.log(`Author ${i}:`, authors[i]);
  console.log(`Rate ${i}:`, rates[i].toString());
}
```
