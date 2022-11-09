# Subscribe to Groups

Users need to opt-in to a group to receive notifications from it. 

Why? Imagine if anyone could send notifications to anyone else. That would be a spammer's paradise.

There are several ways to ask users to opt-in to a group.

## Using the DApp
The easiest method is to ask them to use the JustPush DApp. 

## Using the SDK (Gassless)
But sometimes you want to ask users to opt-in to a group from your own DApp. In that case, you can use the JustPush SDK.

Before continuing you might want to check out the setting up SDK guide. Make sure to pass the `tronWeb` object from `window.tronWeb` to the `JustPush` constructor.

{% content-ref url="../developer-resources/sdk.md" %}
[sdk.md](../developer-resources/sdk.md)
{% endcontent-ref %}

Once you have set up your SDK, you can use the `subscribe` function as follows.

```typescript

// tronweb comes from client side. 
// Users will be prompted to sign a transaction to opt-in to the group.
const justPush = new JustPush(window.tronWeb as any);

const main = async () => {
  await justPush.sendNotification({
    {
      groupId: 'GroupID you noted down earlier',
  });
  console.log('User subscribed');
}
```

## Using Smart Contract

You can also use the JustPush smart contract and call `subscribe` method directly.

```solidity
IJustPushV1(JUSTPUSH_CONTRACT_ADDRESS).subscribe(
    "cb5edeb6-a8a1-466a-aa6c-0d01d88fa68e", // groupId
);
```

This will use the `tx.origin` adress as the user who is subscribing. 

&#x20;You can find **JUSTPUSH\_CONTRACT\_ADDRESS** on Mainnet or Testnet in the [Smart Contracts Guide](../developer-resources/smart-contracts.md).

