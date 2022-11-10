---
description: This section explains the Smart Contract of JustPush protocol.
---

# Smart Contracts

You can find the full smart contract code [here](https://github.com/justpush-protocol/contracts).

Deployed contract addresses:

Mainnet: **`TMptrmkFrmvc3zHV7c62kHAFka44Ae5ob1`**

The contract is made of 3 interfaces.

### IJustPushV1.sol

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.6;

interface IJustPushV1 {
    /**
     * @notice Initializes the protocol.
     * @param _justPushGovernance The address of the JustPush governance.
     */
    function initialize(address _justPushGovernance) external;

    /**
     * @notice Creates a new notification group.
     * @param _id A unique identifier for the group.
     * @param _owner Owner of the group.
     * @param _data A Json string that holds the group name, description, and other metadata.
     */
    function createGroup(
        string memory _id,
        address _owner,
        string memory _data
    ) external;

    /**
     * @notice Adds a new notifier to the group.
     * @param _groupId The id of the group.
     * @param _notifier The address of the notifier.
     */
    function addNotifier(string memory _groupId, address _notifier) external;

    /**
     * @notice Removes a notifier from the group.
     * @param _groupId The id of the group.
     * @param _notifier The address of the notifier.
     */
    function disableNotifier(string memory _groupId, address _notifier)
        external;

    /**
     * @notice Changes the group owner.
     * @param _groupId The id of the group.
     * @param _newOwner The address of the new owner.
     */
    function changeGroupOwner(string memory _groupId, address _newOwner)
        external;

    /**
     * @notice Deactivates a group.
     * @param _groupId The id of the group.
     */
    function deactivateGroup(string memory _groupId) external;

    /**
     * @notice Activates a group.
     * @param _groupId The id of the group.
     */
    function activateGroup(string memory _groupId) external;

    /**
     * @notice Blocks a group.
     * @param _groupId The id of the group.
     */
    function blockGroup(string memory _groupId) external;

    /**
     * @notice Verifies a group.
     * @param _groupId The id of the group.
     */
    function verifyGroup(string memory _groupId) external;

    /**
     * @notice Unverifies a group.
     * @param _groupId The id of the group.
     */
    function unverifyGroup(string memory _groupId) external;

    /**
     * @notice Verifies batch of groups.
     * @param _groupIds The ids of the groups.
     */
    function batchVerifyGroups(string[] memory _groupIds) external;

    /**
     * @notice Subscribes a user to a group.
     * @param _groupId The id of the group.
     */
    function subscribe(string memory _groupId) external;

    /**
     * @notice Batch subscribe a user to multiple groups.
     * @param _groupIds The ids of the groups.
     */
    function batchSubscribe(string[] memory _groupIds) external;

    /**
     * @notice Unsubscribes a user from a group.
     * @param _groupId The id of the group.
     */
    function unsubscribe(string memory _groupId) external;

    /**
     * @notice Batch unsubscribe a user from multiple groups.
     * @param _groupIds The ids of the groups.
     */
    function batchUnsubscribe(string[] memory _groupIds) external;

    /**
     * @notice Changes the JustPush governance.
     * @param _newGovernance The address of the new governance.
     */
    function changeGovernace(address _newGovernance) external;

    /**
     * @notice Find out if an address is a notifier of a group.
     * @param _groupId The id of the group.
     * @param _notifier The address of the notifier.
     */
    function isNotifier(string memory _groupId, address _notifier)
        external
        view
        returns (bool);
}
```

### IBroadcastNotificationSender

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.6;

// Use this interface to send broadcast notifications to JustPush.
interface IBroadcastNotificationSender {
    /**
     * @notice Sends a broadcast notification to JustPush.
     * @param _groupId The id of the group.
     * @param _title The title of the notification.
     * @param _content The body of the notification.
     */
    function sendBroadcastNotification(
        string memory _groupId,
        string calldata _title,
        string calldata _content
    ) external;
}
```

### IDirectNotificationSender

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.6;

// Use this interface to send notifications to a subscrber directly.
interface IDirectNotificationSender {
    /**
     * @notice Send notification to a group.
     * @param _groupId The id of the group.
     * @param _receiver The address of the receiver.
     * @param _title The title of the notification.
     * @param _content The content of the notification.
     */
    function sendNotification(
        string memory _groupId,
        address _receiver,
        string calldata _title,
        string calldata _content
    ) external;
}
```
