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

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../">Guides and Tutorials</a></td><td><a href="../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../assets/physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../assets/ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% embed url="https://kb.heathenengineering.com/assets/steamworks/ugui-tools" %}

You can list friends, contacts, groups and other collections of Steam users and user groups using the Friends API or our [uGUI Tools for Steam](broken-reference).

Its possible to filter these lists by the type of friend on query from Steam and then in your game's logic you can further filter these lists based on users in game, or not in game, online or offline, etc.

## Groups

{% embed url="https://kb.heathenengineering.com/assets/steamworks/learning/core-concepts/clans" %}

Also know as Clans; Steam's concept of a group or clan or guild is simply a collect of "friends" that is Steam Users. We have split the Groups / Clans system our from Friends in its own set of [API](../../../../assets/steamworks/api/clans.md)s and tools.

## Friend Chat

It is possible to chat with specific friends in game though this is not typical. To get started you would need to enable the [Listen for Friend Messages](../../../../assets/steamworks/api/friends.md#setlistenforfriendsmessages) feature in the [Friend API](../../../../assets/steamworks/api/friends.md). Once this is enabled the [EventGameConnectedFriendChatMsg ](../../../../assets/steamworks/api/friends.md#game-connected-friend-chat-msg)event will be raised when receiving a message from a friend. You can also [Send Messages](../../../../assets/steamworks/data-layer/user-data.md#sendmessage) to friends either via the [User Data](../../../../assets/steamworks/data-layer/user-data.md) object or the [Friend API](../../../../assets/steamworks/api/friends.md).
