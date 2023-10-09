---
cover: ../../../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
---

# 🟩 Lobby Game Server

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Represents the known "Game Server" information for a given lobby.&#x20;

### Is Set

True if the data is set, false otherwise

### IP

The IP address if set, otherwise empty

### Port

The connection port if set otherwise 0

### Game Server ID

The Steam ID of the user or Steam game server acting as the host if defined, otherwise 0.

{% hint style="info" %}
In a Peer to Peer (P2P) setup, this will be the Steam ID of the user running the listen server.\
\
In a Client / Server setup, this will be the Steam ID of the Steam Game Server.
{% endhint %}

## Nodes

<figure><img src="../../../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
