# Projects

Papaya supports project separation, as the protocol was originally designed for platforms rather than individual users.

To utilize this functionality, call the `claimProjectId` method to assign a unique identifier to your wallet. This ID is necessary for users of your platform and for configuring both general and specific settings for individual users.

```solidity
function claimProjectId() external
```

{% hint style="info" %}
Invoke this method from the wallet where the commission should be directed.
{% endhint %}

### Settings

The `Settings` structure defines whether settings are applied and specifies the fee amount. It is formatted as follows:

```solidity
struct Settings {
  bool initialized;
  uint16 projectFee; // of 10k shares
}
```

### setDefaultSettings

Set the default fee settings for all users within your project.

```solidity
function setDefaultSettings(Settings calldata settings, uint256 projectId)
```

***

### setSettingsForUser

Allows precise configuration of fees for a specific user, useful for scenarios such as collaborating with key opinion leaders.

```solidity
function setSettingsForUser(address user, Settings calldata settings, uint256 projectId)
```

***

{% hint style="warning" %}
These methods enable the management and fine-tuning of user fee settings for your project. Note that the maximum fee is capped at 20% of the authors’ income on your platform.
{% endhint %}
