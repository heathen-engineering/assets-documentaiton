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

# 🔵 Get Lobby Data

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Gets the metadata associated with the specified key from the specified lobby.

{% hint style="info" %}
This can only get metadata from lobbies that the client knows about, either after receiving a list of lobbies from a query, retrieving the data with Request Lobby Data or after joining a lobby.
{% endhint %}

### Lobby Id

The lobby ID to read data from

### Key

The key to the data to read

### Return Value

The value stored for that key in the lobby if any

## Nodes

<figure><img src="../../../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
