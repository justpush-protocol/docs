---
description: This section describes several ways to send notifications.
---

# Sending Notifications

Ensure your group is set up properly following the guide and note down your `groupid`.

{% content-ref url="create-group.md" %}
[create-group.md](create-group.md)
{% endcontent-ref %}

You have to be either an `owner` or a `notifier` of a group to be able to send notifications.

There are two types of notifications.

1. Broadcast notification - Send a notification to all subscribers (ex: proposal, news)
2. Direct notification - Send notification to one wallet address (ex: dapp notifications)

JustPush provides multiple ways to send notifications.

## Using Smart Contract

Start by importing one of the following interfaces depending on the type of notification you are sending.

```solidity
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

```solidity
// Use this interface to send notifications to a subscriber directly.
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

Next, call the function specified in the interface with notification content and the `groupId` you noted down earlier.

In the following example. We are sending a broadcast notification.

```solidity
IBroadcastNotificationSender(JUSTPUSH_CONTRACT_ADDRESS).sendBroadcastNotification(
    "cb5edeb6-a8a1-466a-aa6c-0d01d88fa68e", // groupId
    "Hello there" // title
    "Welcome to JustPush" // content
);
```

You can find **JUSTPUSH\_CONTRACT\_ADDRESS** on Mainnet in the [Smart Contracts Guide](../developer-resources/smart-contracts.md).

## Using the SDK (Gassless)

Before continuing you might want to check out the setting up SDK guide.

{% content-ref url="../developer-resources/sdk.md" %}
[sdk.md](../developer-resources/sdk.md)
{% endcontent-ref %}

Once you have set up your SDK, you can send notifications to the groups you manage by `sendNotification` function.

`sendNotification` takes an object of type `AddNotificationRequest.`

```typescript
export interface AddNotificationRequest {
    id: string; // random unique id
    groupId: string; // group id you are sending the notification to
    to: string | undefined; // user you are sending notification to, `undefined` for broadcast notifications
    notification: NotificationContent; // content of the notification
    broadcast: boolean; // true if the notification is a broadcast notification
    self: boolean; // true if the notification is sent to yourself, 
    timestamp: number; // timestamp of the notification in seconds
}

export interface NotificationContent {
    title: string | null | undefined; // title for the notification
    content: string; // content of the notification
    link: string | null | undefined; // a link to your dapp/service
}
```

In the following example, We are sending a broadcast notification.

```typescript
import {v4 as uuidv4} from 'uuid';
const justPush = new JustPush(tronWeb);

const main = async () => {
  await justPush.sendNotification({
    {
      id: uuidv4(), // some random id
      groupId: 'The group id you are sending your message to',
      to: undefined,
      notification: {
        title: 'Hi there,
        content: 'Welcome to JustPush',
        link: 'justpush.app',
      },
      broadcast: true,
      self: false,
      timestamp: (Date.now())/1000,
  });
  console.log('Notification sent');
}
```
