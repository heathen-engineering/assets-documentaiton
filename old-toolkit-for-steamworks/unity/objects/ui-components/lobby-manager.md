---
description: Lobby management made easy
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Lobby Manager

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

The Lobby Manager ... not to be confused with Steamworks V1 Lobby Manager ... is a tool for creating and managing a specific lobby.&#x20;

This component is meant to be attached to a game object in your matchmaking scene / ui. Your game may have multiple Lobby Managers where each manages a single specific lobby.

{% hint style="info" %}
The Lobby Manager is a simple Unity component (MonoBehaviour) that simplifies manging a specific lobby. That is this tool does not magically managage all lobbies it only manages the lobby it is connected to.



You connect a lobby to the LobbyManager by using the LobbyManager to create or join said lobby or by setting the LobbyManager.Lobby field to the lobby you want it to manage.
{% endhint %}

### Steam Lobby

The [Steam Lobby](../../../../company/steam/steamworks/multiplayer/matchmaking-tools.md) feature of the Steam API is a flexible and powerful tool useful for far more than simple matchmaking. We find it best to think of a "lobby" more like a chat room with metadata. It does not have anything to do with networking, it doesn't have to relate to a game session or a game server.

Steam allows a player to be apart of up to 3 lobbies but has a few restrictions.

*   The player may only be apart of 1 "**normal**" lobby.

    Steam defines a normal lobby as any lobby which is not of type "**Invisible**"
*   The player may be apart of up to 2 "**invisible**" lobbies

    An indivisible lobby doesn't appear on player's rich presence or Friends list displays (Public and Friend Only do). It is however possible to search for invisible lobbies so you can allow player's to browse for them.&#x20;

### Lobby Types

The following explains; as clearly as Steam documentation allows, the available lobby types and when and how you might use them.

*   Private

    Classified as a "**Normal**" lobby by Steam.

    The only way to join a private lobby is to be invited to it via the Lobby.InvitePlayer feature. This can be useful in coop games when your player want to play with a specific friend but doesn't want to be bothered by requests to join or public searches.

    This lobby will not appear in searches, it will not appear on the user's friends list or rich presence data.
*   Friends Only

    Classified as a "**Normal**" lobby by Steam.

    This lobby can only be joined by friends of the owner or by people directly invited to it. This lobby does appear on the user's friends list but does not appear in lobby lists or searches. This is useful when the player wants friends to be able to drop in / out but doesn't want be bothered by random players.
*   Public

    Classified as a "**Normal**" lobby by Steam.

    This is the typical lobby you will see used in most games. Its the classic "Matchmaking" lobby that appears on the user's friends list and can be searched for and joined by any matching player.
*   **Invisible**

    This is the lobby type that Valve/Steam allows a user to be a member of 2 of

    This lobby is not visible in the friends list but can be searched for. That might be confusing at first read.

    A random user can search for this lobby as you would a public lobby but this lobby will not show up on the Steam Friends list hence "invisible"

### Heathen Constant Data

Steam Lobby is a wonderful tool but it has a few glaring gaps that are often requested. To support the most commonly requested of these gaps Heathen has developed extensions of Steam Lobby.

{% hint style="info" %}
We do this by managing lobby metadata.&#x20;

It is possible to get this data out of sync if you use the raw Steam API. Using our API wrapper e.g. API.Matchmaking will preserve these values.
{% endhint %}

You can learn more about these extension features in the [Lobby](../classes/lobby-data.md) article.

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class LobbyManager : MonoBehaviour
```

## Events

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

You can add events via the Add New Event Type button in a manner similar to Unity's Event Trigger component. The names listed are slightly different from the names as they appear in code to help clarify the use of each when IntelliSense is not available as it is in code.

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### evtFound

```csharp
public LobbyDataListEvent evtFound
```

Occurs when a search for matchmaking lobbies returns. The handler would be similar to the following.

```csharp
private void Handler(LobbyData[] lobbies)
{
    //Do work
}
```

### evtEnterSuccess

```csharp
public LobbyDataEvent evtEnterSuccess
```

Occurs when the local user enters a lobby as the result of a join request. The handler would be similar to the following.

```csharp
private void Handler(LobbyData lobby)
{
    //Do work
}
```

### evtEnterFailed

```csharp
public LobbyResponceEvent evtEnterFailed
```

Occurs when the local user attempts to enter a lobby but gets an invalid enter response. The handler would be similar to the following.

```csharp
private void Handler(EChatRoomEnterResponse responce)
{
    //Do work
}
```

### evtCreated

```csharp
public LobbyDataEvent evtCreated
```

Occurs when a lobby is created. The handler would be similar to the following.

```csharp
private void Handler(LobbyData lobby)
{
    //Do work
}
```

### evtCreateFailed

```csharp
public EResultEvent evtCreateFailed
```

Occurs when an attempt to create a lobby fails. The handler would be similar to the following.

{% hint style="info" %}
Learn more about [EResult ](https://partner.steamgames.com/doc/api/steam_api#EResult)in Valve's documentation [here](https://partner.steamgames.com/doc/api/steam_api#EResult).
{% endhint %}

```csharp
private void Handler(EResult result)
{
    //Do work
    Debug.LogError($"Lobby Create failed with error code: {result}");
}
```

### evtQuickMatchFailed

```csharp
public UnityEvent evtQuickMatchFailed
```

Occurs when an attempt to find a quick match failed and was not allowed to create a lobby on completion. The handler would be similar to the following.

```csharp
private void Handler()
{
    //Do work
}
```

### evtDataUpdated

```csharp
public LobbyDataUpdateEvent evtDataUpdated
```

Occurs when the lobby's metadata or the metadata on a lobby member is updated. The handler would be similar to the following.

```csharp
private void Handler(LobbyDataUpdate_t dataUpdated)
{
    if(dataUpdated.m_ulSteamIDLobby == dataUpdated.m_ulSteamIDMember)
    {
        //It was lobby data that was updated
    }
    else
    {
        //It was this member that updated
        var member = new LobbyMember
                { 
                    lobby = dataUpdated.m_ulSteamIDLobby,
                    user = dataUpdated.m_ulSteamIDMember
                };
    }
}
```

### evtLeave

```csharp
public UnityEvent evtLeave
```

Occurs when the local user leaves the lobby. The handler would be similar to the following.

```csharp
private void Handler()
{
    //Do work
}
```

### evtAskedToLeave

```csharp
public UnityEvent evtAskedToLeave
```

Occurs when the local user is asked to leave the lobby via the Kick system. The handler would be similar to the following.

```csharp
private void Handler()
{
    //Do work
}
```

### evtGameCreated

```csharp
public GameServerSetEvent evtGameCreated
```

Occurs when the lobby owner set's the game server data on the lobby. This is raised on all members but not on the owner of the lobby. As the owner is the one that sets this they already know. The handler would be similar to the following.

```csharp
private void Handler(LobbyGameServer server)
{
    //Do work
}
```

### evtUserJoined

```csharp
public UserDataEvent evtUserJoined
```

Occurs when the local user is a member of a lobby and a new user joins that lobby. The handler would be similar to the following.

```csharp
private void Handler(UserData user)
{
    //Do work
}
```

### evtUserLeft

```csharp
public UserLeaveEvent evtUserLeft
```

Occurs when the local user is a member of a lobby and a fellow member leaves the lobby. The handler would be similar to the following.

```csharp
private void Handler(UserLobbyLeaveData user)
{
    //Do work
}
```

## Fields and Attributes

### SearchArguments

```csharp
public SearchArguments searchArguments;
```

Used with any form of search performed through the Lobby Manager including the [Search](lobby-manager.md#search) and [QuickMatch ](lobby-manager.md#quick-match)methods. This is used to define the "search arguments" e.g. the rules to be tested when searching for lobbies.

The `SearchArguments` data type is an internal class:

```csharp
[Serializable]
public class SearchArguments
{
    /// <summary>
    /// If less than or equal to 0 then we wont use the open slot filter
    /// </summary>
    public int slots = -1;
    public ELobbyDistanceFilter distance = ELobbyDistanceFilter.k_ELobbyDistanceFilterDefault;
    public List<NearFilter> nearValues = new List<NearFilter>();
    public List<NumericFilter> numericFilters = new List<NumericFilter>();
    public List<StringFilter> stringFilters = new List<StringFilter>();
}
```

The fields of the class are as follows

* slots\
  If less than or equal to 0 this will be ignored otherwise this will indicate the number of available slots resulting lobbies must have. For example if you wanted to find a lobby for you and 3 friends then you would provide a value of 4 in this field to return only lobbies that had 4 open slots.
* distance\
  An enumerator that indicates the max alowed distance between the searching user and the members of the resulting lobbies. For more details on the values see [Valve's documentation on ELobbyDistanceFilter](https://partner.steamgames.com/doc/api/ISteamMatchmaking#ELobbyDistanceFilter), in summary
  * Close\
    Only in the same Valve region as this user
  * Default\
    In the same or near by Valve region as this user
  * Far\
    Up to half a world away&#x20;
  * World Wide\
    No filtering at all
* nearValues\
  Key value pairs that the system should search for "near by" values for. See [Valve's documentation](https://partner.steamgames.com/doc/api/ISteamMatchmaking#AddRequestLobbyListNearValueFilter) on this feature for more details. In summary this doesn't "filter out" lobbies but rather effects the sorting, the closer a lobby's metadata is to matching this value the higher it will be sorted in the resulting list. This is useful for say "Player Rank" whose min and max player rank is as near the player's actual rank as possible. To do this you could set near values of `minRank = myRank` and `maxRank = myRank` this would not exclude any lobbies in and of its self but would sort lobbies such that top results where nearest "my rank" ... this assumes minRank is the rank of the lowest ranked player in that lobby and maxRank is the rank of the highhest ranked player in that lobby
* numericFilters\
  Instructs the search to perform a numeric filtering operation on these fields and can filer by the following methods
  * Equal to or Less than
  * Less than
  * Equal
  * Greater than
  * Equal to or Greater thhan
  * Not Equal
* stringFilter\
  Instructs the search to perform a string filtering operation on these fields and can be filtered by the same methods as numeric filters. Valve doesn't explain what the result of each is so test to confirm desired results.

### CreateArguments

```csharp
public CreateArguments createArguments;
```

Used by the Lobby Manager any time a lobby is created with it, this would apply to [Create ](lobby-manager.md#create)as well as [QuickMatch ](lobby-manager.md#quick-match)when no lobby is found and create on fail is set to true.

The `CreateArguments` data type is an internal class:

```csharp
[Serializable]
public class CreateArguments
{
    public UseHintOptions usageHint;
    public string name;
    public int slots;
    public ELobbyType type;
    public List<MetadataTempalate> metadata = new List<MetadataTempalate>();
}
```

the fields of the class are as follows

* usageHint\
  This simply indicates what the intended use is for the lobbies created by this instance of the lobby manager. If set to a value other than "None" it will cause the Lobby Manager on Create of a new lobby to set that lobby as either Group or Session depending on the value you set here.
* name\
  This will be set as metadata on the lobby when created e.g. \
  `MyLobby["name"] = value;`
* slots\
  This is the maximum number of slots this lobby will have ... this is including the owner of the lobby.
* type\
  The type of lobby to create, you can learn more about the [available types above](lobby-manager.md#lobby-types).
* metadata\
  Metadata fields to be set on the lobby once created. This is a simple string key and string value pairing. Metadata is what is used when "filtering" or "searching" for lobbies.

### Lobby

```csharp
public LobbyData Lobby { get; set; }
```

The lobby the manager is currently managing. This will automatically be updated when you use the lobby manager to create, join or leave a lobby. If you create, join or leave a lobby from outside the manager then you should update this field accordingly.

### HasLobby

```csharp
public bool HasLobby => get;
```

True if the manager is managing a lobby, false otherwise.

### IsPlayerOwner

```csharp
public bool IsPlayerOwner => get;
```

True if the local user is the owner of the managed lobby, false otherwise.

### AllPlayersReady

```csharp
public bool AllPlayersReady => get;
```

True if all members of the lobby have marked them selves as ready, otherwise false.

### IsPlayerReady

```csharp
public bool IsPlayerReady { get; set; }
```

Returns true if the player has marked them self as ready on this lobby. This can be set to mark the player as ready or not on this lobby.

### Full

```csharp
public bool Full => get;
```

Returns true if the lobby is currently full, false otherwise.

### IsTypeSet

```csharp
public bool IsTypeSet => get;
```

Returns true if the lobby type has been recorded on the lobby metadata, false otherwise.

### Type

```csharp
public ELobbyType Type { get; set; }
```

Returns the type of lobby this lobby is set to, this is a feature of Heahten's Lobby tools. Valve does not actually expose this so this will only work for lobbies created by Heathen's tools such as the lobby manager or the API.Matchmaking class. This can only be set by the owner of the lobby.

### MaxMembers

```csharp
public int MaxMembers { get; set; }
```

Indicates the max number of members that can be in the lobby. This can be set by the owner of the lobby to change the max slots.

### HasServer

```csharp
public bool HasServer => get;
```

Returns true if the lobby has had its game server set, false otherwise.

### GameServer

```csharp
public LobbyGameServer GameServer => get;
```

Returns data about the game server set on the lobby if any.

## Methods

### Set Type

```csharp
public bool SetType(ELobbyType type);
```

Funcitonally the same as setting the Type field. This updates the type of the lobby on Valve's backend and updated the value of DataType. See the [Lobby](../classes/lobby-data.md) object article for more information on DataType.

### Set Joinable

```csharp
public bool SetJoinable(bool makeJoinable);
```

Sets the lobby if any, as joinable or not

### Quick Match

```csharp
public void QuickMatch(bool createOnFail = true);
```

Searches for a match based on the Search Arguments set on the object. If a match is found it will join that first lobby. If no match is found and createOnFail is set to true then the process will create a new lobby. If no match is found and createOnFail is set to false then the process will invoke the Quick Match Failed event.

### Create

```csharp
public void Create();
```

Creates a new lobby with the data found in the Create Argument.

### Search

```csharp
public void Search(int maxResults);
```

Searches for lobbies that match the Search Arguments set on the object. This will always invoke the evtFound event which will pass in an array of the lobby found if any.

### Join

```csharp
public void Join(LobbyData lobby);
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

### Leave

```csharp
public void Leave();
```

Does what it says on the tin and simply leaves the lobby clearning the managed lobby ID in the process.

### Set Lobby Data

```csharp
public bool SetLobbyData(string key, string value);
```

If the local user is the owner of the lobby this will set the related metadata field on the lobby. Otherwise this returns false.

### Set Member Data

```csharp
public SetLobbyMemberData(string key, string value);
```

If in a lobby this will set the user's metadata value corasponding to this key.

### Invite

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

To learn more about Heathen Constant Data such as DataType pleaes read the [Lobby ](../classes/lobby-data.md)object article.

The DataType matadata value is the enumerator value of each of the Steam [ELobbyTypes](https://partner.steamgames.com/doc/api/ISteamMatchmaking#ELobbyType) e.g.&#x20;

* 0 = Private
* 1 = Friends Only
* 2 = Public
* 3 = Invisible

The Type feild on the Lobby and the Lobby Manager will reutrn the current type if known, if not known it will return a default of 0 = private. You can use Lobby.IsTypeSet or LobbyManager.IsTypeSet to determin if the value is known.

### Lobby Chat

See the [Lobby Chat Director](lobby-chat-director.md) componenet for details
