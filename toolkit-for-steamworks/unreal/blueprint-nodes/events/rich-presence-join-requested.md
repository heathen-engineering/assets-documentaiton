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

# 🔻 Rich Presence Join Requested

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Called when the user tries to join a game from their friends list or after a user accepts an invite by a friend with [InviteUserToGame](../functions/invite-user-to-game.md).

{% hint style="info" %}
This callback is made when joining a game. If the user is attempting to join a lobby, then the callback [Lobby Join Requested](lobby-join-requested.md) will be made.
{% endhint %}

### Steam Id

The friend they joined through. This will be invalid if not directly via a friend.

### Connection String

The value associated with the "connect" Rich Presence key or provided by the inviting user on the request.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (224).png" alt=""><figcaption></figcaption></figure>
