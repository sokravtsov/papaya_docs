---
description: >-
  This section covers the functions for creating and managing streaming
  subscriptions between users.
---

# Subscription Management

### subscribe

Creates a subscription to stream tokens to an author.

```solidity
function subscribe(address author, uint96 subscriptionRate, uint256 projectId) external
```

#### Parameters

* `author` (address): The address of the content creator to subscribe to
* `subscriptionRate` (uint96): The rate of tokens to stream per second
* `projectId` (uint256): The ID of the project for this subscription

#### Description

Creates a subscription that streams tokens from the caller to the specified author at the given rate. The subscription is associated with a specific project ID for fee management.

#### Example

```javascript
// Subscribe to an author at 0.001 tokens per second for project 1
await papayaContract.subscribe(
  "0xauthor...",
  ethers.utils.parseEther("0.001"),
  1
);
```

### unsubscribe

Cancels a subscription to an author.

```solidity
function unsubscribe(address author) external
```

#### Parameters

* `author` (address): The address of the author to unsubscribe from

#### Description

Cancels an active subscription to the specified author. This stops the token streaming immediately.

#### Example

```javascript
// Unsubscribe from an author
await papayaContract.unsubscribe("0xauthor...");
```

### Related Events

* [StreamCreated](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/subscription-events#streamcreated): Emitted when a subscription is created
* [StreamRevoked](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/subscription-events#streamrevoked): Emitted when a subscription is cancelled

### Related Errors

* [NotSubscribed](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#notsubscribed): When trying to unsubscribe from a non-existent subscription
* [ExcessOfRate](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#excessofrate): When subscription rate exceeds limits
* [ExcessOfSubscriptions](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#excessofsubscriptions): When user has too many active subscriptions
