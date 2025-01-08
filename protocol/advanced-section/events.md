# Events

***

This event emits when certain project sets general settings by its owner

```solidity
event SetDefaultSettings(uint256 indexed projectId, uint16 protocolFee);
```

***

This event emits when certain projects sets sets settings for certain user by owner of projectId

```solidity
event SetSettingsForUser(uint256 indexed projectId, address indexed user, uint16 protocolFee);
```

{% hint style="info" %}
Note this is convenient when you work with someone who has special needs about how much percentage of the revenue they will pay you
{% endhint %}

***

This event emits every time when every subscription created

```solidity
event StreamCreated(address indexed user, address indexed author, uint256 indexed encodedRates);
```

{% hint style="info" %}
Note this event is really useful if you want to create your own backend, because of it you can track every subscription of entire smart-contract and do what you need.
{% endhint %}

***

This event emits every time when every subscription ended, it can be done with user or liquidator

```solidity
event StreamRevoked(address indexed user, address indexed author, uint256 indexed encodedRates);
```

***

This event emits every time when somebody is liquidated

```solidity
event Liquidated(address indexed user, address indexed liquidator);
```

{% hint style="success" %}
You can check our explanation of liquidations here:
{% endhint %}

{% content-ref url="../liquidations.md" %}
[liquidations.md](../liquidations.md)
{% endcontent-ref %}

***

This event emits every time when native token and our abstract token moves

```solidity
event Transfer(address indexed _from, address indexed _to, uint256 _value);
```

***

This event emits every time when somebody takes his own projectId

```solidity
event ProjectIdClaimed(uint256 projectId, address admin);
```
