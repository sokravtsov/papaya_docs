---
description: This section covers the view functions for querying project information.
---

# Project Queries

### projectOwners

Gets the owner of a specific project ID.

```solidity
function projectOwners(uint256) external view returns (address)
```

#### Parameters

* `projectId` (uint256): The project ID

#### Returns

* `owner` (address): The project owner's address

#### Description

Returns the owner address for a specific project ID.

#### Example

```javascript
// Get project owner
const owner = await papayaContract.projectOwners(1);
console.log("Project 1 owner:", owner);
```

### allProjectOwners

Gets all project owners.

```solidity
function allProjectOwners() external view returns (address[])
```

#### Returns

* `owners` (address\[]): Array of all project owner addresses

#### Description

Returns an array of all project owner addresses.

#### Example

```javascript
// Get all project owners
const owners = await papayaContract.allProjectOwners();
console.log("Number of projects:", owners.length);
owners.forEach((owner, index) => {
  console.log(`Project ${index} owner:`, owner);
});
```

### defaultSettings

Gets the default settings for a project.

```solidity
function defaultSettings(uint256 projectId) external view returns (bool initialized, uint16 projectFee)
```

#### Parameters

* `projectId` (uint256): The project ID

#### Returns

* `initialized` (bool): Whether the settings are initialized
* `projectFee` (uint16): The project fee percentage

#### Description

Returns the default settings for a specific project.

#### Example

```javascript
// Get default project settings
const [initialized, projectFee] = await papayaContract.defaultSettings(1);
console.log("Settings initialized:", initialized);
console.log("Project fee:", projectFee, "basis points");
```

### userSettings

Gets the custom settings for a user in a specific project.

```solidity
function userSettings(uint256 projectId, address account) external view returns (bool initialized, uint16 projectFee)
```

#### Parameters

* `projectId` (uint256): The project ID
* `account` (address): The user's address

#### Returns

* `initialized` (bool): Whether the settings are initialized
* `projectFee` (uint16): The project fee percentage

#### Description

Returns the custom settings for a specific user in a specific project.

#### Example

```javascript
// Get user settings for project
const [initialized, projectFee] = await papayaContract.userSettings(1, "0xuser...");
console.log("User settings initialized:", initialized);
console.log("User project fee:", projectFee, "basis points");
```
