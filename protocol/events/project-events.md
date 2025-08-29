---
description: This section covers the events related to project management.
---

# Project Events

### ProjectIdClaimed

Emitted when a project ID is claimed.

```solidity
event ProjectIdClaimed(uint256 projectId, address admin)
```

#### Parameters

* `projectId` (uint256): The claimed project ID
* `admin` (address): The address that claimed the project ID

#### Description

Emitted when a project ID is claimed through the `claimProjectId` function.

#### Example

```javascript
// Listen for project ID claim events
papayaContract.on("ProjectIdClaimed", (projectId, admin) => {
  console.log(`Project ID ${projectId} claimed by ${admin}`);
});
```

### SetDefaultSettings

Emitted when default project settings are updated.

```solidity
event SetDefaultSettings(uint256 indexed projectId, uint16 protocolFee)
```

#### Parameters

* `projectId` (uint256, indexed): The project ID
* `protocolFee` (uint16): The protocol fee percentage

#### Description

Emitted when default settings are updated for a project through the `setDefaultSettings` function.

#### Example

```javascript
// Listen for default settings update events
papayaContract.on("SetDefaultSettings", (projectId, protocolFee) => {
  console.log(`Default settings updated for project ${projectId} with fee ${protocolFee}`);
});
```

### SetSettingsForUser

Emitted when user-specific project settings are updated.

```solidity
event SetSettingsForUser(uint256 indexed projectId, address indexed user, uint16 protocolFee)
```

#### Parameters

* `projectId` (uint256, indexed): The project ID
* `user` (address, indexed): The user's address
* `protocolFee` (uint16): The protocol fee percentage

#### Description

Emitted when user-specific settings are updated for a project through the `setSettingsForUser` function.

#### Example

```javascript
// Listen for user settings update events
papayaContract.on("SetSettingsForUser", (projectId, user, protocolFee) => {
  console.log(`User settings updated for project ${projectId}, user ${user} with fee ${protocolFee}`);
});
```
