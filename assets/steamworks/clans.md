---
description: Tools and features specific to Steam Clans aka Steam Groups.
---

# Clans

## Introduction

The Steam Clan, aka Steam Group system is part of Valve's Steam Friend system. Player's can freely create clans which work similar to guilds in MMOs in that they have a roster, officers, can run events and have a dedicated chat system that is always accessible to members.

{% hint style="danger" %}
Valve and Heathen strongly recommend that you handle Clan chat via the Steam Overlay.

Steam Clan chats can be very large and handling feeds from many sources, each of which the player may be an active member of. The Steam API has many limitations when dealing with Steam Clan chat in the Steam Client API, and is not likely to perform well for large Clans.
{% endhint %}

Heathen's Clan Tools simplify Valve's clan interface features. It maintains a list of the player's clans and each clans member ship which can be refreshed on demand. Clan chat can be interacted with through code, though in general its advised to use the Steam Overlay as Clan chat can be very complex on account of the large number of users and that a player may interact with the chat from a wide range of sources such as Steam Client, Web Browser, Mobile App, Overlay or of 3rd party apps and games.

## Examples

### Browse the list of clans

The list of clans is loaded on initialization of the Steam system and can be accessed via the clans member

```csharp
var listOfClans = SteamSettings.Client.clanTools.clans;
```

You can force a refresh of the clans list via

```csharp
SteamSettings.Client.clanTools.RefreshClanList();
```

### Get data about a clan

The clans listed in the clans list are of type `SteamClan` and define the following details of a clan

```csharp
public CSteamID id;
public string displayName;
public string tagString;
public UserData Owner;
public List<UserData> Officers;
```

### Open the clan chat

This is the strongly recommended method of handling clan chat. Note this will open the Steam Overlay to this clan's chat.

For a specific clan such as

```csharp
var clan = SteamSettings.Client.clanTools.clans[0];
```

Then you can use

```csharp
clan.OpenChat();
```

### Get clan chat members

This has limitations as defined by Valve at the link below

{% embed url="https://partner.steamgames.com/doc/api/ISteamFriends#GetClanChatMemberCount" %}

It is strongly recommended that you use the "OpenChat" feature of the clan as opposed to attempting to manage a large chat in game.

For a specific clan such as

```csharp
var clan = SteamSettings.Client.clanTools.clans[0];
```

You can list the members in a chat up to the limits of Valve's APIs via the following code. Note that this will return a `List<UserData>` object

```csharp
var listOfMembers = clan.GetChatMembers();
```

### Join clan chat

This will enable callbacks. Please note the repeated warning from Valve and Heathen that you should use Steam Overlay for clan chat.

Using a specific clan as noted above

```csharp
clan.JoinChat();
```

### Leaving clan chat

Using a specific clan as noted above

```csharp
clan.LeaveChat();
```

Once done you should be listening on the `chatMessageRecieved` event to handle incoming chat messages

```csharp
clan.chatMessageReceived.AddListener(HandleIncomingMessage);
```

where

```csharp
private void HandleIncomingMessage(UserData user, string message, EChatEntryType type)
{
    //DO WORK
}
```

### Send clan chat message

Using a specific clan as noted above

```csharp
clan.SendChatMessage("Hello Clan!");
```

