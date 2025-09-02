---
description: This section covers the functions for managing project settings and fees.
hidden: true
---

# Project Management

### claimProjectId

Claims a project ID for a project owner.

```solidity
function claimProjectId(address projectOwner) external
```

#### Parameters

* `projectOwner` (address): The address of the project owner

#### Description

Allows a project owner to claim a unique project ID. This ID is used for managing project-specific settings and fees.

#### Example

```javascript
// Claim project ID for a project owner
await papayaContract.claimProjectId("0xprojectOwner...");
```

### setDefaultSettings

Sets the default settings for a project.

```solidity
function setDefaultSettings(Settings memory settings, uint256 projectId) external
```

#### Parameters

* `settings` (Settings): The settings struct containing:
  * `initialized` (bool): Whether the settings are initialized
  * `projectFee` (uint16): The project fee percentage
* `projectId` (uint256): The ID of the project

#### Description

Sets the default fee settings for a specific project. These settings apply to all users who don't have custom settings for this project.

#### Example

```javascript
// Set default settings for project 1 with 5% fee
await papayaContract.setDefaultSettings(
  {
    initialized: true,
    projectFee: 500 // 5% = 500 basis points
  },
  1
);
```

### setSettingsForUser

Sets custom settings for a specific user in a project.

```solidity
function setSettingsForUser(address user, Settings memory settings, uint256 projectId) external
```

#### Parameters

* `user` (address): The user address to set settings for
* `settings` (Settings): The settings struct containing:
  * `initialized` (bool): Whether the settings are initialized
  * `projectFee` (uint16): The project fee percentage
* `projectId` (uint256): The ID of the project

#### Description

Sets custom fee settings for a specific user in a specific project. These settings override the default project settings for this user.

#### Example

```javascript
// Set custom settings for user in project 1 with 3% fee
await papayaContract.setSettingsForUser(
  "0xuser...",
  {
    initialized: true,
    projectFee: 300 // 3% = 300 basis points
  },
  1
);
```

### Related Events

* [ProjectIdClaimed](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/project-events#projectidclaimed): Emitted when a project ID is claimed
* [SetDefaultSettings](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/project-events#setdefaultsettings): Emitted when default settings are updated
* [SetSettingsForUser](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/events/project-events#setsettingsforuser): Emitted when user settings are updated

### Related Errors

* [InvalidProjectId](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#invalidprojectid): When project ID is invalid
* [AccessDenied](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#accessdenied): When caller doesn't have permission to set settings
* [WrongPercent](https://app.gitbook.com/o/qmYNDgxzLtvTeLBHbPpz/s/crhGDzgi59PyfFaJtlVP/~/changes/67/protocol/error-codes#wrongpercent): When fee percentage is invalid
