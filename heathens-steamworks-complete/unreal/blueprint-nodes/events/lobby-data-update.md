---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# 🔻 Lobby Data Update

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

A chat (text or binary) message for this lobby has been received. After getting this you must use [Get Lobby Chat Entry](../functions/get-lobby-chat-entry.md) to retrieve the contents of this message.

### Lobby Id

The ID of the lobby applies to

### Subject

The ID of the subject for whom the data changed, if this is the same as the Lobby ID then the lobby's metadata changed, else it was a member and this is the member Steam ID

### Sucess

Was the update of data a success or not, this is false when Request Lobby Data was called on an invalid lobby.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
