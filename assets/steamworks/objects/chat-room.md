---
description: Represents a Clan Chat Room
---

# Chat Room

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct ChatRoom
```

The clan chat room structure is used by chat specific features of the Clans interface and is its self a shortcut to the most common chat features.

## Fields and Attributes

| Type                   | Name          | Comment                                                                                     |
| ---------------------- | ------------- | ------------------------------------------------------------------------------------------- |
| Clan                   | clan          | The clan this room belongs to                                                               |
| CSteamID               | id            | The id of the room                                                                          |
| EChatRoomEnterResponse | enterResponce | The responce from Steam when the user attempted to enter the room if any                    |
| UserData\[]            | Members       | The list of chat members, note client interface cannot iterate the full list of large clans |
| bool                   | IsOpenInSteam | Check if the chat is open in Steam UI                                                       |

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
