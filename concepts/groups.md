# What are Groups?

A `Group` is a service that can send notifications to its users. A `Group` can be a DApp, a service or any other entity that wants to send notifications to its users.

Any service that wants to send notifications to their users can create a `Group.`Typically dApps in the Tron ecosystem will create a `Group` to send notifications to their users.

The creation of a group happens on-chain. A channel can have one `owner` and multiple `notifiers`. Only the owner of the group can add or remove notifiers. Only `owners` and `notifiers` can send notifications to the group.

A successfully created `Group` is capable of sending notifications to its subscribers directly. These notifications are tied to the subscriber's wallet address. Any wallet address can become a `subscriber` of the Group by opting in.

> Ideally, in the future there will be staking requirement to create groups so the protocol is not congested with spam groups. But as of right now, there is no such requirement.


{% content-ref url="../developer-guides/create-group.md" %}
[create-group.md](../developer-guides/create-group.md)
{% endcontent-ref %}
