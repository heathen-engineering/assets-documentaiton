---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🔵 Join Lobby

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Invite another user to the lobby.\
\
If the specified user clicks the join link, a [Game Lobby Join Requested](../friends/lobby-join-requested.md) callback will be posted if the user is in-game, or if the game isn't running yet then the game will be automatically launched with the command line parameter `+connect_lobby <64-bit lobby Steam ID>` instead.

### Lobby Id

The Steam ID of the lobby to invite the user to

### Callback

An event that will be called when the process completes and will indicate the results of the request.

* Lobby Id\
  The lobby joined
* Blocked\
  Was the join request blocked such as from other members of the lobby, VAC, etc.
* Response\
  The [UEChatRoomEnterResponse ](../enumerators/uechatroomenterresponse.md)response to the user joining the lobby

## Nodes

<figure><img src="../../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>
