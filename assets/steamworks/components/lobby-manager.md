---
description: Lobby management made easy
---

# Lobby Manager

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

## Introduction

The Lobby Manager ... not to be confused with Steamworks V1 Lobby Manager ... is a tool for creating and managing a specific lobby.&#x20;

This componenet is meant to be attached to a game object in your matchmaking scene / ui. Your game may have multiple Lobby Managers where each manages a single specific lobby.

### Steam Lobby

The Steam Lobby feature of the Steam API is a flexable and powerful tool useful for far more than simple matchmaking. We find it best to think of a "lobby" more like a chat room with metadata. It does not have anything to do with networking, it doesn't have to relate to a game session or a game server.

Steam allows a player to be apart of up to 3 lobbies but has a few restrictions.

*   The player may only be apart of 1 "normal" lobby.

    Steam defines a normal lobby as any lobby which is not of type "Invisible"
*   The player may be apart of up to 2 "invisible" lobbies

    An inivisible lobby doesn't appear on player's rich presence or Friends list displays (Public and Friend Only do). It is however possible to search for invisible lobbies so you can allow player's to browse for them.&#x20;

### Lobby Types

The following explains; as clearly as Steam documentaiton allows, the available lobby types and when and how you might use them.

*   Private

    Classified as a "Normal" lobby by Steam.

    The only way to join a private lobby is to be invited to it via the Lobby.InvitePlayer feature. This can be useful in coop games when your player want to play with a specific friend but doens't want to be bothered by requests to join or public searches.

    This lobby will not appear in searches, it will not appear on the user's friends list or rich presence data.
*   Friends Only

    Classified as a "Normal" lobby by Steam.

    This lobby can only be joined by friends of the owner or by people directly invited to it. This lobby does appear on the user's friends list but does not appear in lobby lists or searches. This is useful when the player wants friends to be able to dorp in / out but doesn't want be bothered by random players.
*   Public

    Classified as a "Normal" lobby by Steam.

    This is the typical lobby you will see used in most games. Its the classic "Matchmaking" lobby that appears on the user's friends list and can be searched for and joined by any matching player.
*   Invisible

    This is the lobby type that Valve/Steam allows a user to be a member of 2 of

    This lobby is not visible in the friends list but can be searched for. That might be confusing at first read.

    A random user can search for this lobby as you would a public lobby but this lobby will not show up on the Steam Friends list hence "invisible"

### Heathen Constant Data

Steam Lobby is a wonderful tool but it has a few glaring gaps that are offten requested. To support the most commonly requested of these gaps Heathen has developed extensions of Steam Lobby.

{% hint style="info" %}
We do this by managing lobby metadata.&#x20;

It is possible to get this data out of sync if you use the raw Steam API. Using our API wrapper e.g. API.Matchmaking will preserve these values.
{% endhint %}

You can learn more about these extension features in the [Lobby](../objects/lobby.md) article.

## Definition

### Fields and Attributes

| Type                                                                            | Name            | Comment                                                                                                                                      |
| ------------------------------------------------------------------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| ulong                                                                           | lobbyId         | The id of the current lobby if known, ID.Nil if not                                                                                          |
| Search Arguments                                                                | searchArguments | Defines the arguments to be used for lobby searches                                                                                          |
| Create Arguments                                                                | createArguments | Defines the arguments to be used when creating a new lobby                                                                                   |
| Lobby                                                                           | Lobby           | The Heathen Lobby object matching the current lobbyId if any                                                                                 |
| bool                                                                            | HasLobby        | True if lobbyId is valid and relates to an active Steam Lobby                                                                                |
| bool                                                                            | IsPlayerOwner   | True if the local user is the owner of the lobby                                                                                             |
| bool                                                                            | AllPlayersReady | True if all player's have reported ready using the Heathen Ready Check feature. See the [Lobby](../objects/lobby.md) object for more details |
| bool                                                                            | Full            | True if the lobby member count is or is higher than the lobby member max                                                                     |
| bool                                                                            | IsTypeSet       | True if the Heathen Type feature is set on this lobby. See the [Lobby ](../objects/lobby.md)object for more details.                         |
| [ELobbyType](https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs) | Type            | Returns the type set in the Heathen Type feature or defaults to priivate if not set. See the Lobby object for more details.                  |
| int                                                                             | MaxMembers      | Returns the max members allowed in this lobby                                                                                                |
| bool                                                                            | HasServer       | Returns true if the lobby game server has been set                                                                                           |
| Lobby Game Server                                                               | GameServer      | Gets details about the lobby game server if set                                                                                              |

### Events

#### evtFound

Occurs when a search for matchming lobbies returns

#### evtJoined

Occurs when a lobby is joined

#### evtCreated

Occurs when a lobby is created

#### evtCreateFailed

Occurs when an attempt to create a lobby fails

#### evtQuickMatchFailed

Occurs when an attempt to find a quick match failed and was not allowed to create a lobby on completion.

### Methods

```csharp
public bool SetType(ELobbyType type);
```

Funcitonally the same as setting the Type field. This updates the type of the lobby on Valve's backend and updated the value of DataType. See the [Lobby](../objects/lobby.md) object article for more information on DataType.

```csharp
public bool SetJoinable(bool makeJoinable);
```

Sets the lobby if any, as joinable or not

```csharp
public void QuickMatch(bool createOnFail = true);
```

Searches for a match based on the Search Arguments set on the object. If a match is found it will join that first lobby. If no match is found and createOnFail is set to true then the process will create a new lobby. If no match is found and createOnFail is set to false then the process will invoke the Quick Match Failed event.

```csharp
public void Create();
```

Creates a new lobby with the data found in the Create Argument.

```csharp
public void Search(int maxResults);
```

Searches for lobbies that match the Search Arguments set on the object. This will always invoke the evtFound event which will pass in an array of the lobby found if any.

```csharp
public void Join(Lobby lobby);
```

```csharp
public void Join(ulong lobby);
```

```csharp
public void Join(string lobbyIdAsString);
```

{% hint style="warning" %}
The string paramiter version only exists so that Unity Inspector can work with the method when using Unity Actions (such as button click). Unfortunetly Unity in all of its wizdome decided that ulong and really anything other than float, int and string cannot be used as paramiters for methods.



You should only use this overload when using Unity Inspector and you should insure that the value is a valid ulong.
{% endhint %}

Joins the indicated lobby

```csharp
public bool SetLobbyData(string key, string value);
```

If the local user is the owner of the lobby this will set the related metadata field on the lobby. Otherwise this returns false.

```csharp
public SetLobbyMemberData(string key, string value);
```

If in a lobby this will set the user's metadata value corasponding to this key.

```csharp
public bool Invite(UserData user);
```

Invites the user to the lobby

## Use

### Player Party / Group

Want to create a party system where player's can invite there friends before finding a match ... similar to what you see in DOTA, TF2, CSGO, etc.?

Create a UI to show your party members and to help the user send invites to or join friend's existing lobbies. You will use a Lobby Manager to help you manage this "party lobby" for example, as this is a "party lobby" you will want it to be of type "Invisible" and so would set the Create Arguments accordingly.

Want to enable a party chat on this lobby?

Simple add a Lobby Chat Director to the same game object you applied the Lobby Manager to, this Chat Director component will help you manage chat for this specific lobby.

### Game Lobby

What to start a match / battle / session, that is you want to gather together players based on some matchmaking logic to start a gameplay session?

Create a UI to show your player there search and creation options and use a Lobby Manager to help you manage this "game lobby". In this case you probably want this to be a public lobby or perhaps you will let the player create friends only, private, etc. types of lobbies.&#x20;

Want to enable lobby chat?

Simply add a Lobby Chat Director to the same game object you applied the Lobby Manager to, this Chat Director componenet will help you manage chat for this specific lobby.

### Team Lobby

Some games use teams which allow a subset of the matched players to chat and update make decisions in a way that can only be seen by there fellow team mebers. You can think of this as a "sub lobby" to a typical "Game Lobby".

To do so, create your Team UI and apply a Lobby Manager to it, this lobby manager will be set to Type Invisible and can have its own Lobby Chat Director to enable team chat. Your Game Lobby will be used to assign player's to teams and provide them with the nessisary information to join the appropreate team.

## FAQ

### Restrict Party Lobby

A party lobby is typically of type Invisible, this type of lobby does apper in lobby searches. The simplest way to remove them from a search is to filter on Lobby.DataType aka "z\_heathenType".

To learn more about Heathen Constant Data such as DataType pleaes read the [Lobby ](../objects/lobby.md)object article.

The DataType matadata value is the enumerator value of each of the Steam [ELobbyTypes](https://partner.steamgames.com/doc/api/ISteamMatchmaking#ELobbyType) e.g.&#x20;

* 0 = Private
* 1 = Friends Only
* 2 = Public
* 3 = Invisible

The Type feild on the Lobby and the Lobby Manager will reutrn the current type if known, if not known it will return a default of 0 = private. You can use Lobby.IsTypeSet or LobbyManager.IsTypeSet to determin if the value is known.

### Lobby Chat

See the [Lobby Chat Director](lobby-chat-director.md) componenet for details
