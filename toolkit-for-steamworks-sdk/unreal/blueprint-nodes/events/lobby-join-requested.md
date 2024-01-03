---
cover: ../../../../.gitbook/assets/Unreal Banner@2x.png
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

# 🔻 Lobby Join Requested

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Called when the user tries to join a lobby from their friend's list or from an invite. The game client should attempt to connect to the specified lobby when this is received. If the game isn't running yet then the game will be automatically launched with the command line parameter `+connect_lobby <64-bit lobby Steam ID>` instead.

### Lobby Id

The Steam ID of the lobby to connect to.

### User Id

The friend they joined through. This will be invalid if not directly via a friend.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (740).png" alt=""><figcaption></figcaption></figure>
