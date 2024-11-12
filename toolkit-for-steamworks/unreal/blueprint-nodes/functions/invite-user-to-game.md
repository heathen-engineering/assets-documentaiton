---
cover: ../../../../.gitbook/assets/Unreal Banner.jpg
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

# 🔵 Invite User To Game

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Invites a friend or clan member to the current game using a special invite string.\
\
If the target user accepts the invite then the pchConnectString gets added to the command-line when launching the game.\
If the game is already running for that user, then they will receive a [GameRichPresenceJoinRequested\_t](https://partner.steamgames.com/doc/api/ISteamFriends#GameRichPresenceJoinRequested\_t) callback with the connect string.

### User ID (Input)

The user you want to invite

### Connection String (input)

The connection string you want to send that friend

### Return Value

True if the invite was successfully sent

False under the following conditions:

* The User ID provided was invalid.
* The User ID provided is not a friend or does not share the same Steam Group as the current user.
* The value provided to the Connection String was too long.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

