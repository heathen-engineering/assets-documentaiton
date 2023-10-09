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

# 🔵 Send Lobby Chat

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Broadcasts a chat (text or binary data) message to the all of the users in the lobby.\
\
All users in the lobby (including the local user) will receive a [Lobby Chat Msg](lobby-chat-msg.md) callback with the message.\
\
If you're sending binary data, you should prefix a header to the message so that you know to treat it as your custom data rather than a plain old text message.\
\
For communication that needs to be arbitrated (for example having a user pick from a set of characters, and making sure only one user has picked a character), you can use the lobby owner as the decision maker. [Get Lobby Owner](get-lobby-owner.md) to return the current lobby owner. There is guaranteed to always be one and only one lobby member who is the owner. So for the choose-a-character scenario, the user who is picking a character would send the binary message 'I want to be Zoe', the lobby owner would see that message, see if it was OK, and broadcast the appropriate result (user X is Zoe).\
\
These messages are sent via the Steam back-end, and so the bandwidth available is limited. For higher-volume traffic like voice or game data, you'll want to use the [Steam Networking API](https://partner.steamgames.com/doc/features/multiplayer/networking).

### Lobby Id

The Steam ID of the lobby to send the chat message to.

### Data / Message

Up to 4 kilobytes of text or byte data

## Nodes

<figure><img src="../../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>
