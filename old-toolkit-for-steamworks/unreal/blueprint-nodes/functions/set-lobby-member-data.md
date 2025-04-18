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

# 🔵 Set Lobby Member Data

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Sets per-user metadata for the local user.

{% hint style="info" %}
A user can only set their own data but can read all other member's data.
{% endhint %}

Each user in the lobby will receive notification of the lobby data change via a [Lobby Data Update](../events/lobby-data-update.md) callback, and any new users joining will receive any existing data.\
\
There is a slight delay before sending the data so you can call this repeatedly to set all the data you need to and it will automatically be batched up and sent after the last sequential call.

### Lobby Id

The ID of the lobby to set the user's data on

### Key

The key of the data to set

### Value

The value of the data to set

## Nodes

<figure><img src="../../../../.gitbook/assets/image (12) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
