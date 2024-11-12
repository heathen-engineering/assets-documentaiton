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

# 🔵 Set Lobby Game Server

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
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

You have 4 ways you can set this data depending on what kind of information you want to store and for what use.&#x20;

For example in a traditional Peer-to-Peer set up aka "Listen Server" the lobby owner is the "host" aka server and so we do not need any info thus the `Set Lobby Listen Server` doesn't require any input other than the server to set it on.

In a multiplex dedicated server, you may want to support Steam ID, as well as IP:Port and so the `Set Lobby Dedicated Server - ID and IP Address` is the option you want. In all cases these will all cause the same event to be raised for the members of the lobby.

<figure><img src="../../../../.gitbook/assets/image (430).png" alt=""><figcaption></figcaption></figure>
