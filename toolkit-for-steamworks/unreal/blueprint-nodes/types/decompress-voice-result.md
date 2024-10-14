---
cover: ../../../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
---

# 🟩 Decompress Voice Result

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Returned by Get Lobby Chat Entry this structure defines the user who sent the message, the data of the message and the type of the message.

### Success

Was the process completed successfully

### Result

The [UEResult](../enumerators/ueresult.md) value of the process

### Decompressed Voice Data

The array of bytes representing the decompressed and ready-to-play voice data that was added to the Procedural Sound Wave

### Procedural Sound Wave

A reference to the same soundwave that was passed in or the new sound wave if null pointer was passed in. This can be played to playback the voice data.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
