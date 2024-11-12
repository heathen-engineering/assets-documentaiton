---
cover: ../../../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
---

# 🔻 Lobby Chat Msg

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

A chat (text or binary) message for this lobby has been received. After getting this you must use [Get Lobby Chat Entry](../functions/get-lobby-chat-entry.md) to retrieve the contents of this message.

### Lobby Id

The ID of the lobby this message was sent in.

### User Id

The ID of the user who sent this message.&#x20;

{% hint style="info" %}
Yes, you will receive messages you sent ... e.g. this can be the local user.
{% endhint %}

### Type

The [UEChatEntryType ](../enumerators/uechatentrytype.md)of the message

### Index

The index of the message, use this with [Get Lobby Chat Entry](../functions/get-lobby-chat-entry.md) to retrieve the contents of the message.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (18) (1) (1).png" alt=""><figcaption></figcaption></figure>
