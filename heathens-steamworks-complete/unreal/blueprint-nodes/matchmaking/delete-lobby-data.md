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

# 🔵 Delete Lobby Data

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Removes a metadata key from the lobby.

This can only be done by the owner of the lobby.

This will only send the data if the key exists. There is a slight delay before sending the data so you can call this repeatedly to set all the data you need to and it will automatically be batched up and sent after the last sequential call.

### Lobby Id

The ID of the lobby to delete the metadata for

### Key

The key to delete the data for

## Nodes

<figure><img src="../../../../.gitbook/assets/image (12) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
