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

# 🔵 Set Lobby Game Server

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Sets the game server associated with the lobby.

This can only be set by the owner of the lobby.

Either the IP/Port or the Steam ID of the game server must be valid, depending on how you want the clients to be able to connect.

{% hint style="info" %}
This will raise the [Lobby Game Created](../events/lobby-game-created.md) callback for all members.\
\
Once this has been set any new members can read the data by using [Get Lobby Game  Server](get-lobby-game-server.md).
{% endhint %}

## Nodes

<figure><img src="../../../../.gitbook/assets/image (6) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Assumes the lobby Owner is the "listen serer" aka "host"</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (7) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Records the provided Server ID as the target server, this can be a user or a Steam Game Server ID</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (8) (1) (1) (1) (1).png" alt=""><figcaption><p>Records an ID, IP Address and Port for the traget server</p></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption><p>Records IP Address and Port for the target server, leaving Server ID default (0)</p></figcaption></figure>
