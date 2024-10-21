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

# 🔵 Get Lobby Game Server

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Gets information about the "game server" for this lobby.&#x20;

{% hint style="info" %}
This is used in both Peer-to-peer and Client-server network setups. In the case of Peer-to-peer, the connection information will be to the "Listen Server" e.g. the user acting as the server, and for a Client-Server setup, it will be to the server.
{% endhint %}

### Lobby Id

The lobby ID to read data from

### Return Value

A [Lobby Game Server](../types/lobby-game-server.md) struct represents the connection information.

## Nodes

<figure><img src="../../../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
