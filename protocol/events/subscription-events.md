---
description: This section covers the events related to subscription management.
---

# Subscription Events

### StreamCreated

Emitted when a subscription is created.

```solidity
event StreamCreated(address indexed user, address indexed author, uint256 indexed encodedRates)
```

#### Parameters

* `user` (address, indexed): The subscriber's address
* `author` (address, indexed): The author's address
* `encodedRates` (uint256, indexed): The encoded subscription rates

#### Description

Emitted when a new subscription is created through the `subscribe` function.

#### Example

```javascript
// Listen for stream creation events
papayaContract.on("StreamCreated", (user, author, encodedRates) => {
  console.log(`Stream created: ${user} subscribed to ${author} with rates ${encodedRates}`);
});
```

### StreamRevoked

Emitted when a subscription is cancelled.

```solidity
event StreamRevoked(address indexed user, address indexed author, uint256 indexed encodedRates)
```

#### Parameters

* `user` (address, indexed): The subscriber's address
* `author` (address, indexed): The author's address
* `encodedRates` (uint256, indexed): The encoded subscription rates

#### Description

Emitted when a subscription is cancelled through the `unsubscribe` function.

#### Example

```javascript
// Listen for stream revocation events
papayaContract.on("StreamRevoked", (user, author, encodedRates) => {
  console.log(`Stream revoked: ${user} unsubscribed from ${author} with rates ${encodedRates}`);
});
```
