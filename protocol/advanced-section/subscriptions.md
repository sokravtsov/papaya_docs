# Subscriptions

***

### allSubscriptions

To retrieve the subscriptions of a specific user, use the `allSubscriptions` method. It returns arrays containing addresses and encoded subscription data (cost, author’s share, project number).

```solidity
function allSubscriptions(address from) external view returns(address[] memory to, uint256[] memory encodedRates)
```

***

### subscriptions

To obtain encoded data for a specific subscription, use the `subscriptions` method. It returns two values: a flag indicating presence and encoded data if the subscription exists.

```solidity
function subscriptions(address from, address to) external view returns (bool, uint256 encodedRates)
```

```solidity
bool - success flag:
    - true subscription exists
    - false in another way
    
uint256 encodedRates - compressed data that stores:
    - uint96 incomeRate
    - uint96 outgoingRate 
    - uint96 projectId 
```

{% hint style="info" %}
Note: incomeRate is a rate that incoming to the author, and outgoingRate is a rate that incoming from the subscriber
{% endhint %}

***

### users

To get information about a user, use the `users` method. This returns four fields: balance, incoming stream, outgoing stream, and the last synchronization timestamp.

```solidity
function users(address) public view returns (User calldata user)
```

```solidity
struct User {
  int256 balance;
  int256 incomeRate; // changes to this field requires _syncBalance() call
  int256 outgoingRate; // changes to this field requires _syncBalance() call
  uint256 updated;
}
```

***

{% hint style="info" %}
Note that balance synchronization occurs on request, so the balance data may be outdated.
{% endhint %}

{% hint style="warning" %}
To calculate the balance yourself, determine the difference between incoming and outgoing streams and multiply by the time elapsed since the last synchronization timestamp. Alternatively, use the balanceOf method for up-to-date data.
{% endhint %}
