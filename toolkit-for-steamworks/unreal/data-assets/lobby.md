---
cover: ../../../.gitbook/assets/Unreal Banner.jpg
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

# Lobby

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Steam's Lobby is an incredibly flexible and often misunderstood feature. We have [articles dedicated to it](../../../company/steam/steamworks/multiplayer/matchmaking-tools.md) so here we will focus just on the use of the Data Asset.

The 1st thing is why you might want a Data Asset for a Lobby. As you likely understand, a Lobby is a dynamically created and used and generally temporary thing so it might not make since at first as to why you would want a Data Asset in your game content for a lobby.

Think of the Lobby Data Asset not as a specific Lobby but as a lobby's role in your game. Most games will have 2 different roles for a Lobby to fill. You can create a Lobby Data Asset for each of these and use that Data Asset to persist information about the lobby as long as you require.

The 2 most common roles/uses of lobbies we see in games are.

### Session Lobby

This is the lobby you use for matchmaking, its where players join up before the game session has started where they may agree on modes, maps, choices, etc. and where the owner of the lobby can advertise when the server (listen or dedicated) is ready to receive connections.

### Group Lobby

This is a lobby used to group friends together, such as a party, fireteam, etc. Take a MOBA as an example 2 teams of players complete. Friends will often "group" or "party" up then look for a match where they can play together.&#x20;

The group is not all the players but is a group of friends that should persist even when the session is over so they might find a new session to join after.

## Create

To creat a new Lobby Data Asset Instance, select the LobbyDataAsset as its type.

<figure><img src="../../../.gitbook/assets/image (438).png" alt=""><figcaption></figcaption></figure>

## Configure

Unlike most DataAssets we don't actually have anything to configure at development time for this lobby, we just want the "slot" so to speak so we can store data here at run time.

## Use

First you will want to reference your lobby so you can easily access it in Blueprint, to do this create a new variable of type LobbyDataAsset.

<figure><img src="../../../.gitbook/assets/image (439).png" alt=""><figcaption></figcaption></figure>

Now we have a variable where we can store the ID of any lobby we join or create. This being a Data Asset it will not be cleared when we change levels so this will persist for us.

### Create a Lobby

<figure><img src="../../../.gitbook/assets/image (440).png" alt=""><figcaption></figcaption></figure>

### Join a Lobby

<figure><img src="../../../.gitbook/assets/image (441).png" alt=""><figcaption></figcaption></figure>

### General Information

Once you have a valid lobby ID ... you read all sorts of data from the lobby to understand the state of it and its members

<figure><img src="../../../.gitbook/assets/image (444).png" alt=""><figcaption></figcaption></figure>

### Metadata

The owner of the lobby can store additional data on the lobby as metadata, each member of the lobby can store data on the lobby about themselves as well. You can use this to handle ready checks, to store player choices, create voting systems and much more.

{% hint style="info" %}
It's the Metadata on the Lobby set by the owner that the Lobby Search feature looks at and compares to filter out and sort lobbies when searching.
{% endhint %}

#### Lobby Metadata

Can be read by anyone, but only set by the owner of the lobby. Note that "Name" is just metadata with the key of `name` it's so commonly used however that we gave it its own function to set and read it.&#x20;

<figure><img src="../../../.gitbook/assets/image (446).png" alt=""><figcaption></figcaption></figure>

#### Your Member Metadata

Only you can set your member metadata, and only your peers within this lobby can read it.

<figure><img src="../../../.gitbook/assets/image (447).png" alt=""><figcaption></figcaption></figure>

#### Reading Their Metadata

<figure><img src="../../../.gitbook/assets/image (448).png" alt=""><figcaption></figcaption></figure>

### Invite and Share

Players can browse for lobbies to join, more commonly however they would "Quick Match" that is they would search for a lobby given search arguments based on the lobby metadata and simply join the first result returned.

When you want to get into a specific lobby however you can either be Invited or provided with the Lobby ID that your player can type in.

#### Invite to Lobby

<figure><img src="../../../.gitbook/assets/image (449).png" alt=""><figcaption></figcaption></figure>

#### Sharable Lobby ID&#x20;

A lobby ID is what Valve would call a CSteamID ... you can learn more about that here ... but in general, its an unsigned int64 which is a long cumbersome number. We have a means to reduce that to an int32 and send it to Hex to make it a bit more human friendly. You can do this with any Steam ID using our tools but we have it built into the Lobby Data Asset as well.

<figure><img src="../../../.gitbook/assets/image (450).png" alt=""><figcaption></figcaption></figure>

And of course, you can use our tools to convert a Hex ID back to the related Steam ID so you can work with it as a proper ID.

<figure><img src="../../../.gitbook/assets/image (452).png" alt=""><figcaption></figcaption></figure>

### Set Game Server

This is used to let the members of the lobby know when the game server (Listen or Dedicated) is ready to be connected to.&#x20;

<figure><img src="../../../.gitbook/assets/image (442).png" alt=""><figcaption></figcaption></figure>

Only the "owner" of the lobby can call these methods, when they are called it will cause the global event Lobby Game Created to be called.&#x20;

<figure><img src="../../../.gitbook/assets/image (443).png" alt=""><figcaption></figcaption></figure>
