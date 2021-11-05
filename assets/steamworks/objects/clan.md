---
description: Representing a Steam Clan aka Steam Group
---

# Clan

{% hint style="warning" %}
Coming Soon

This will be released with Patch 13 and is expected late 2021 to early 2022 as a free update to Steamworks V2
{% endhint %}

## Definition

```csharp
public struct Clan
```

The clan structure is used by most of the features of the API.Clans interface. Its returned by GetClans and similar methods and is an input for most methods.

The Clan structure is interchangable with CSteamID and ulong

```csharp
Clan clan = new CSteamID(id);
CSteamID clanId = clan;
ulong clanIdValue = clan;
Clan clanCopy = clanIdValue;
```

### Fields and Attributes

| Type        | Name     | Comment                                  |
| ----------- | -------- | ---------------------------------------- |
| CSteamID    | id       | The CSteamID of the clan                 |
| string      | Name     | Returns the name of the clan             |
| string      | Tag      | Returns the tag of the clan              |
| UserData    | Owner    | Returns the owner of the clan            |
| UserData\[] | Officers | Returns the list of officers of the clan |

### Methods

```csharp
public void JoinChat(Action<ClanChatRoom, bool> callback);
```

The JoinChat method will attempt to join the user to clan's chat room. The resulting callback will return a ClanChatRoom object indicating the state, providing access to the chat and being of use in other chat related methods.
