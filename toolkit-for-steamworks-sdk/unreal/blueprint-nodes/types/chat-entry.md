---
cover: ../../../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
---

# 🟩 Chat Entry

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Returned by Get Lobby Chat Entry this structure defines the user who sent the message, the data of the message and the type of the message.

### Data

An array of bytes representing the raw data

### String

A string representation of that data simply handles the data as if it were UTF8 encoded bytes and will only be relevant if it was a string that was sent.

### User Id

The ID of the user that sent the message

### Type

The [UEChatEntryType ](../enumerators/uechatentrytype.md)of the message

## Nodes

<figure><img src="../../../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>
