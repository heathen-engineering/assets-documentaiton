---
description: Represents a Clan Chat Room
---

# Chat Room

{% hint style="warning" %}
Coming Soon

This will be released with Patch 13 and is expected late 2021 to early 2022 as a free update to Steamworks V2
{% endhint %}

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

```csharp
public bool SendMessage(string message);
```

Attempts to send a message to the chat.

```csharp
public bool OpenChatWindowInSteam();
```

Opens the clan chat in the Steam UI ... this is generally recomended especially for large clans as opposed to creating an in game clan chat.

```csharp
public void Leave();
```

Leaves the clan chat if the user is in it
