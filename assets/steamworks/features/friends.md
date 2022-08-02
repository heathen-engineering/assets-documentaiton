---
description: List your user friends, open chats, send invites and much more!
---

# Friends

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

The Friends API provides access to all of the user data related features of Steam and is not restricted to users that are the local user's "friends".

Using the Friends API you can list users, gather data on them, read the rich presence data from them and set the local user's data.

By in large the [UserData](../objects/user-data.md) object provides a simpler method for working with the [Friends API](../api/friends.md) however we also have a Unity centric Friends API wrapper.

## User Data

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/user-data" %}
Read Me!
{% endembed %}

Heathen's [UserData](../objects/user-data.md) is a simple struct and can be used implicitly as a CSteamID or ulong value and provides a lot of quality of life features dealing with Steam User Data such as accessing the local user, getting display or nick names, getting avatar images, setting rich presence data, inviting to game or lobby and so much more.

## Lists

{% embed url="https://kb.heathenengineering.com/assets/steamworks/ugui-tools" %}

You can list friends, contacts, groups and other collections of Steam users and user groups using the Friends API or our [uGUI Tools for Steam](../ugui-tools/).

Its possible to filter these lists by the type of friend on query from Steam and then in your game's logic you can further filter these lists based on users in game, or not in game, online or offline, etc.

## Groups

{% embed url="https://kb.heathenengineering.com/assets/steamworks/learning/core-concepts/clans" %}

Also know as Clans; Steam's concept of a group or clan or guild is simply a collect of "friends" that is Steam Users. We have split the Groups / Clans system our from Friends in its own set of [API](../api/clans.md)s and tools.

## Friend Chat

It is possible to chat with specific friends in game though this is not typical. To get started you would need to enable the [Listen for Friend Messages](../api/friends.md#setlistenforfriendsmessages) feature in the [Friend API](../api/friends.md). Once this is enabled the [EventGameConnectedFriendChatMsg ](../api/friends.md#game-connected-friend-chat-msg)event will be raised when receiving a message from a friend. You can also [Send Messages](../objects/user-data.md#sendmessage) to friends either via the [User Data](../objects/user-data.md) object or the [Friend API](../api/friends.md).
