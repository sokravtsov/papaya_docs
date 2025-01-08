# Subscription Methods

***

### pay

Enables the transfer of funds outside the subscription mechanism, akin to a traditional transfer method.

```solidity
function pay(address receiver, uint256 amount)
```

***

### **subscribe**

Allows the creation and modification of subscriptions. Users specify their desired monthly payment amount, as costs cannot be efficiently predefined.

```solidity
function subscribe(address author, uint96 subscriptionRate, uint256 projectId)
```

***

### **unsubscribe**

Trigger the termination of a subscription. This method can be called at any time to halt payments from an individual user.

```solidity
function unsubscribe(address author) external
```
