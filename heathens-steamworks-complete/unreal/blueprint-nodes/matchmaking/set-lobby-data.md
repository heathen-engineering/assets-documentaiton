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

# 🔵 Set Lobby Data

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Sets a key/value pair in the lobby metadata. This can be used to set the lobby name, current map, game mode, etc.\
\
This can only be set by the owner of the lobby. Lobby members should use Set Lobby Member Data instead.\
\
Each user in the lobby will receive notification of the lobby data change via a [Lobby Data Update](lobby-data-update.md) callback, and any new users joining will receive any existing data.\
\
This will only send the data if it has changed. There is a slight delay before sending the data so you can call this repeatedly to set all the data you need to and it will automatically be batched up and sent after the last sequential call.

### Lobby Id

The Steam ID of the lobby to set

### Key

The key of the data to set

### Value

The value of the data to set

### Return Value

True if set successfully, false indicates the lobby ID is invalid or the key/value is to long.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>
