---
description: List your user friends, open chats, send invites and much more!
---

# Friend List

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% embed url="https://kb.heathenengineering.com/assets/steamworks/ugui-tools" %}

You can list friends, contacts, groups and other collections of Steam users and user groups using the Friends API or our [uGUI Tools for Steam](broken-reference).

Its possible to filter these lists by the type of friend on query from Steam and then in your game's logic you can further filter these lists based on users in game, or not in game, online or offline, etc.

## Groups

{% embed url="https://kb.heathenengineering.com/assets/steamworks/learning/core-concepts/clans" %}

Also know as Clans; Steam's concept of a group or clan or guild is simply a collect of "friends" that is Steam Users. We have split the Groups / Clans system our from Friends in its own set of [API](../../../../assets/steamworks/unity-engine/api/clans.client.md)s and tools.

## Friend Chat

It is possible to chat with specific friends in game though this is not typical. To get started you would need to enable the [Listen for Friend Messages](../../../../assets/steamworks/unity-engine/api/friends.client.md#setlistenforfriendsmessages) feature in the [Friend API](../../../../assets/steamworks/unity-engine/api/friends.client.md). Once this is enabled the [EventGameConnectedFriendChatMsg ](../../../../assets/steamworks/unity-engine/api/friends.client.md#game-connected-friend-chat-msg)event will be raised when receiving a message from a friend. You can also [Send Messages](../../../../assets/steamworks/unity-engine/data-layer/user-data.md#sendmessage) to friends either via the [User Data](../../../../assets/steamworks/unity-engine/data-layer/user-data.md) object or the [Friend API](../../../../assets/steamworks/unity-engine/api/friends.client.md).
