---
description: Represents a Clan Chat Room
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Chat Room

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using HeathenEngineering.SteamworksIntegration;
```

```csharp
public struct ChatRoom
```

The clan chat room structure is used by chat-specific features of the Clans interface and is itself a shortcut to the most common chat features.

## Fields and Attributes

<table><thead><tr><th width="193.7178270108939">Type</th><th width="150">Name</th><th width="379.4856019593156">Comment</th></tr></thead><tbody><tr><td>Clan</td><td>clan</td><td>The clan this room belongs to</td></tr><tr><td>CSteamID</td><td>id</td><td>The id of the room</td></tr><tr><td>EChatRoomEnterResponse</td><td>enterResponce</td><td>The responce from Steam when the user attempted to enter the room if any</td></tr><tr><td>UserData[]</td><td>Members</td><td>The list of chat members, note client interface cannot iterate the full list of large clans</td></tr><tr><td>bool</td><td>IsOpenInSteam</td><td>Check if the chat is open in Steam UI</td></tr></tbody></table>

## Methods

### Send Message

```csharp
public bool SendMessage(string message);
```

Attempts to send a message to the chat.

### Open Chat Window

```csharp
public bool OpenChatWindowInSteam();
```

Opens the clan chat in the Steam UI ... this is generally recomended especially for large clans as opposed to creating an in game clan chat.

### Leave

```csharp
public void Leave();
```

Leaves the clan chat if the user is in it
