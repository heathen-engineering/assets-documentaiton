---
description: >-
  Search, Join, Configure and Manage Steam lobbies. Matchmaking tools enables
  player matchmaking, player parties, simple chat and more.
---

# Matchmaking

## Introduction

```csharp
public static class MatchmakingTools
```

The matchmaking tool set can also be accessed via the SteamSettings object, this is done for discover-ability reasons, it is more efficient to use the static class directly.

```csharp
SteamSettings.Client.matchmaking
```

Steam Matchmaking is driven primarily through the Steam Lobby feature. In a nutshell, the concept is that players will create a "lobby". You can think of this a bit like a chat room. This lobby has "metadata" associated with it which can be used to search for lobbies, filtering the results to just those the player cares about.‌

The metadata concept of Steam Lobby is where most of the functionality comes into play. The owner or "host" of a lobby can set the metadata on a lobby and anyone else can read that data, and the Steam Lobby search system can use that data to refine search results. In addition, each member within a lobby has a set of metadata associated with them. Lobby member metadata can only be set by the member it is related to and can only be read by other members of that lobby.‌

In summary lobby metadata is for stating the intent of the session or the status of the session and is accessible by everyone. Member metadata is for stating the intent of a member or the status of a member and is writable only by that member and readable only by fellow members of the same lobby.‌

You can read more about Steam's Matchmaking system on Valve's developer documentation.

{% embed url="https://partner.steamgames.com/doc/features/multiplayer#matchmaking" %}

### MathechmakingTools.memberOfLobbies

```csharp
public static List<Lobby> memberOfLobbies;
```

The memberOfLobbies member is the set of lobbies that the current user is a member of. Valve allows a user to be a member of up to 3 lobbies where only 1 is a "normal" or non-invisible lobby and the other 2 are invisible lobbies.

Invisible lobbies can be used for group or party systems,  to merge multiple lobbies together, etc. Heathen's Matchmaking Tools further defines a concept of "normal" and "group" lobbies where the first invisible lobby is treated as a player group.

### MatchmakingTools.normalLobby

```csharp
public static Lobby normalLobby;
```

The normal lobby is the one and only non-invisible lobby that the local user is a member of (if any). This can be used as a short cut to grab the most commonly used lobby without needing to look up a reference.

#### Examples

```csharp
var myNormalLobby = MatchmakingTools.normalLobby;
```

### MatchmakingTools.groupLobby

```csharp
public static Lobby groupLobby;
```

The group lobby is the first invisible lobby the player joins or creates. It is assumed to represent the player group and is linked for quick access. Note you can declare a lobby to be the "group lobby" by setting the `IsGroup` field. Note this will update the lobby type if required to be invisible.

#### Examples

```csharp
var myGrouplobby = MatchmakingTools.groupLobby;
```

```csharp
lobby.IsGroup = true;
```

## Concepts

The Heathen Matchmaking Tools system simplifies the raw Steam API by creating higher level concepts for common use cases. The following describes these high level concepts in detail.

### Metadata

The concept of metadata applies to both the lobby its self and the members of a lobby. Members and the lobby both contain "metadata", metadata is simply a string dictionary of key and value pairs. Steam uses metadata on the lobby to store common information such as the server conneciton information and you as a developer can use metadata for any information you like assuming it fits in the requirements defined by Valve.

* Max Key Length = 255
* Max Value Length = 8192

The lobby metadata can be read by any Steam user that can "see" the lobby; that would include all members of the lobby and any user that can "browse" for the lobby. For public lobbies that is effectivly all Steam users. Lobby metadata can **only** be set by the owner of the lobby.

The member metadata can **only** be read by fellow members of that lobby. Member metadata can **only** be set by the member its self.

### Lobby

This represents a Steam Lobby and provides access to its respective members. A key concept with Steam Lobby is the presence of "metadata". This is simply a `string` key to `string` value pair used to share information between members of the lobby and used when searching for a lobby.

For example the host of the lobby might storage a metadata value such as `key` = `mapName` and `value` = `cool world` , all members of the lobby would be made aware of this change and be able to read this data reliably thus all members will know the map name has been set to "cool world".

{% hint style="info" %}
Lobby metadata is a powerful system used in matchmaking and player collaboration when configuring the game session to play.&#x20;

Members of a lobby also have metadata associated with them, see the concept of Lobby Member below.
{% endhint %}

#### Examples

Note you first need a reference to the lobby, you could get this from the list of lobbies tracked by the system.

```csharp
var lobby = MatchmakingTools.lobbies[0];
```

Or specific fetch the normal lobby

```csharp
var lobby = MatchmakingTools.normalLobby;
```

Or the group lobby

```csharp
var lobby = MatchmakingTools.groupLobby;
```

Once you have a reference to the lobby you can read the metadata associated with the lobby you can read its metadata via a simple indexer;

```csharp
Debug.Log("Map name: " + lobby["mapName"]);
```

You can set values on lobby metadata in a similar way

```csharp
lobby["mapName"] = "Cool World";
```

{% hint style="warning" %}
Only the owner of a lobby can set lobby metadata

Anyone can read lobby metadata whether or not they are a member of the lobby.
{% endhint %}

To get the ID of the lobby

```csharp
var lobbyId = lobby.id;
```

To get the local user's `LobbyMember` in this lobby

```csharp
var thisUser = lobby.User;
```

To get the `LobbyMember` that owns the lobby e.g. is the host of the lobby

```csharp
var owner = lobby.Owner;
```

To get the type of lobby this lobby is

```csharp
var lobbyType = lobby.Type;
```

To change the lobby type

```csharp
lobby.Type = ELobbyType.k_ELobbyTypeInvisible;
```

{% hint style="warning" %}
Note Valve only allows a member to be part of 1 "normal" lobby at a time.&#x20;

Changing the lobby type can only be performed by the owner of the lobby.

Changing the lobby type will update the `MatchmakingTools.normalLobby` and `MatchmakingTools.groupLobby` if possible.
{% endhint %}

Check if lobby is a group lobby

```csharp
if(lobby.IsGroup)
    ...
```

Change the member limit on the lobby

```csharp
lobby.MemberCountLimit = 42;
```

Check if the local user is the owner aka host of the lobby

```csharp
if(lobby.IsHost)
    ...
```

The host can set the lobby join-able or not, effectively locking or unlocking the lobby regardless of lobby type.

```csharp
lobby.Joinable = false;
```

When the host is ready to start the game and has spun up a server, or is prepared to have members join it in peer to peer it can call `SetGameServer` . This can be called in a few ways depending on what the "server" is. Once set all members will be notified of the data and can react accordingly.

{% hint style="warning" %}
Only the owner / host of a lobby can set the game server.
{% endhint %}

This being set will cause the `evtGameServerSet` event to be raised on the lobby so all members that are listening on that event will be notified

&#x20;for example

```csharp
lobby.evtGameServerSet.AddListener(HandleGameServerSet);
```

For P2P (peer to peer) no parameters are needed, the system will assume the owner/host is the server.

```csharp
lobby.SetGameServer();
```

For Steam Game Server's or to declare a Steam User as the networking host, simply provide the CSteamID of the server or user desired as the input parameter.

```csharp
lobby.SetGameServer(hostId);
//or
lobby.SetGameServer(gameServerId);
```

You can of course also set a traditional server address e.g. an IP and Port

```csharp
lobby.SetGameServer(ipAddress, port);
```

And finally we can set both the ID and traditional addressing

```csharp
lobby.SetGameServer(ipAddress, port, gameServerId);
```

Steam Lobbies include a simple chat system.&#x20;

You can listen for incoming chat messages via the `evtChatMessageReceived` Unity Event

```csharp
lobby.evtChatMessageReceived.AddListener(HandleIncomingChatMessage);
```

The event sends a single parameter of type `LobbyChatMessageData` that will define the chat entry type, the lobby the message came from, the member who sent the message, the time the message was received and the string content of the message.

You can send chat messages via

```csharp
lobby.SendChatMessage("Hello World");
```

Leave the lobby

```csharp
lobby.Leave();
```

As the host you can request that users leave the lobby, and Heathen's tools will automatically have that user leave the lobby. This is a sort of kick system, note that a forced kick system is not permitted by Valve.

```csharp
lobby.KickMember(memberId);
```

To iterate over the list of members that are part of this lobby

```csharp
foreach(var member in lobby.members)
    ...
```

### Lobby Query Parameters

{% hint style="info" %}
#### Code Documentation

[HeathenEngineering.​SteamAPI.​LobbyQueryParameters](https://heathen-engineering.github.io/steamworks-v2-documentation/index.html#CSharpClass:HeathenEngineering.SteamAPI.LobbyQueryParameters)
{% endhint %}

This is a special object used in queries for Steam lobbies. The object defines the search parameters to use and the limitations of search such as distance restrictions or max results to return.

#### Examples

Create a query to find the top 10 lobbies where mapName = Cool World

```csharp
var query = new LobbyQueryParametrs()
{
    maxResults = 10,
    stringValues = 
        { new LobbyQueryStringFiler 
            { 
                key = "mapName",
                value = "Cool World",
                method = ELobbyComparison.k_ELobbyComparisonEqual,
            } 
        }.
};
```

Create a query to find the top 10 lobbies where minRank > 1 and maxRank < 10

```csharp
var query = new LobbyQueryParametrs()
{
    maxResults = 10,
    numberValues = 
        { new LobbyQueryNumericFilter
            { 
                key = "minRank",
                value = 1,
                method = ELobbyComparison.k_ELobbyComparisonGreaterThan,
            },
          new LobbyQueryNumericFilter
            { 
                key = "maxRank",
                value = 10,
                method = ELobbyComparison.k_ELobbyComparisonLessThan,
            }   
        }.
};
```

### Lobby Member

{% hint style="info" %}
#### Code Documentation

[HeathenEngineering.​SteamAPI.​LobbyMember](https://heathen-engineering.github.io/steamworks-v2-documentation/index.html#CSharpClass:HeathenEngineering.SteamAPI.LobbyMember)
{% endhint %}

The Lobby Member object defines the Steam user data for a lobby member as well as the member's lobby metadata. You can access your local user's metadata via

```csharp
var thisIsMe = lobby.User;
```

{% hint style="warning" %}
Only the member itself can set its metadata.

The host cannot set metadata on any member other than its self and the lobby its self.
{% endhint %}

You can set a metadata field on the member via the indexer

```csharp
lobby.User["mapPreference"] = "Cool World";
```

you can read the metadata of any member in the lobby

```csharp
var someOnesChoice = lobby.members[0]["mapPreference"];
```

Heathen has built in a simple "Ready Check" system, this is in reality just metadata. Members can set the Is Ready flag as

```csharp
lobby.User.IsReady = true;
```

The lobby will raise an event anytime a member's data has changed and the overall state of the IsReady can be checked on the lobby

that is to say&#x20;

```csharp
lobby.IsReady
```

will be true if all members have set true to the IsReady value on them selves.

The Lobby Member object contains a normal [User Data](../steam-settings.md#user-data) object containing all the Steam user data for the member.

```csharp
var userData = lobby.members[0].userData;
```

You can get the Lobby Member of the owner of the lobby via

```csharp
var owner = lobby.Owner;
```

## Matchmaking Tools Usage

Note that many methods take a "callback" parameter of type `Action` . A callback action is simply a pointer to a method and can be written as expression.

&#x20;For example, assume a method such as:

```csharp
public void Foo(Action<string> callback)
{
    callback?.invoke("Hello World");
}
```

Callback being an `Action<string>` indicates that it is a pointer to a method that expects 1 parameter of type string. So, we can invoke callback passing it a string. You could call the `Foo` method in a few different ways as expressed below.

```csharp
Foo(HandleFooCallback);
```

This method assumes that `HandleFooCallback` is a method that takes a string as a parameter such as.

```csharp
private void HandleFooCallback(string message)
{
    Debug.Log("Foo says: " + message);
}
```

If you were to pass `HandleFooCallback` into `Foo` as we have shown in the example the printed output would be similar to

`Foo says: Hello World`&#x20;

We could also define the callback method as an expression in-line with the call such as

```csharp
Foo((message) =>
    {
        Debug.Log("Foo says: " + message);
    });
```

This is functionally the same as the previous example and would result in the same output.

### Create a Lobby.

For more information on lobby types see Valve's documentation [https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs](https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs)&#x20;

```csharp
MatchmakingTools.CreateLobby(ELobbyType.k_ELobbyTypePublic,
    memberCount,
    callback);
```

### Create  Group

Groups are simply lobbies of type ` k_ELobbyTypeInvisible` that the system can track in a special use case.

```csharp
MatchmakingTools.CreateGroup(memberCount, callback);
```

### Join Lobby

You will need the lobby ID you wish to join ahead of time, you can get the lobby ID from a friend invite or by browsing for lobbies.

```csharp
MatchmakingTools.JoinLobby(lobbyId, callback);
```

### Find Lobbies

To browse for lobbies you should first create the `LobbyQueryParameters` which is how we filter the results down to the desired set.&#x20;

```csharp
MatchmakingTools.FindLobbies(queryParams, callback);
```

### Send Chat Message

Steam Lobby includes a simple chat system, sending a chat message can be done as

```csharp
MatchmakingTools.SendChatMessage(lobbyId, message);
```

### Invite a Friend to a lobby

First you need to get the lobby you want to invite the friend to.

```csharp
lobby.InviteUserToLobby(userId);
```

Inviting a friend to lobby will do different things depending on the state of the friend. For example if the friend owns the game ,and is currently playing the game, then the `evtGameLobbyJoinRequest` event will be raised. You should have your game listen on this event so you can handle the invite acceptance.

```csharp
MatchmakingTools.evtGameLobbyJoinRequest.AddListener(HandleJoinRequest);
```

The typical use case is that when this event is detected that you gracefully exit whatever you are currently doing and navigate to the Lobby UI, then join the lobby.

{% hint style="info" %}
This event being raised means that the user has clicked accept on the invite and is now expecting that your game is joining that lobby. You generally shouldn't put up any additional barriers such as additional confirmation checks.
{% endhint %}

In the event the invite is accepted and the player is not currently running the game and assuming the player owns the game, then Steam Client will launch the game passing in a command line argument indicating the lobby the user wishes to join.

`+connect_lobby [lobbyid]`

It is up to you to parse for this command line value and handle the process that should follow e.g. to navigate to your lobby UI and then join the indicated lobby.

&#x20;A crude example follows

```csharp
// Return the ulong value of the lobby to join if any
public static ulong GetSteamLobbyInvite()
{
    var args = Environment.GetCommandLineArgs();
    ulong value = 0;
    for (int i = 0; i < args.Length; i++)
    {
        if (args[i] == CommonCommands.SteamLobbyConnect 
            && i + 1 < args.Length 
            && ulong.TryParse(args[i + 1], out value))
            return value;
    }

    return value;
}
```

Then you can perform the following

```csharp
var targetLobby = GetSteamLobbyInvite();
if(targetLobby > 0)
{
    //TODO: navigate to the Lobby UI in your game
    //Join the lobby
    MatchmakingTools.JoinLobby(targetLobby);
}
```

### Get Information about a lobby

When searching for a lobby you and preparing a Lobby Browser like user interface you may want to get at additional information. That is information that was not provided to you by the&#x20;

```csharp
public class LobbyQueryResultList
```

{% hint style="warning" %}
Valve does not allow you to query member data for lobbies you are not a member of. Fore example you can not get the list of users in a lobby nor any information about them.
{% endhint %}

The only "extra" information you can get is via the Lobby metadata system. That is you can read all of the metadata associated with a lobby without being a member of it.

&#x20;Heathen's tools can help you fetch this information quickly via&#x20;

```csharp
LobbyQueryResultList.GetLobbyMetaData(CSteamID id)
```

That is the result list returned has a method on it that will return the dictionary of metadata applied to the indicated lobby.&#x20;

Alternatively each of the values stored in the list contains a metadata member, that is the result list is a list of results

```csharp
public class LobbyQueryResultList : List<LobbyQueryResultRecord>
```

{% hint style="info" %}
LobbyQueryResultList is a list of LobbyQueryResultRecords and so you can for example

```csharp
foreach(var lobby in myLobbyQueryResultList)
...
```
{% endhint %}

So in each result you have the following information

```csharp
public struct LobbyQueryResultRecord
{
    public string name;
    public CSteamID lobbyId;
    public int maxSlots;
    public CSteamID hostId;
    public Dictionary<string, string> metadata;
}
```

### Notify "Connect to network"

The typical purpose of a lobby is to gather player's and settle on the rules and conditions of the multiplayer session. In most cases you will at some point want to notify player's that they should connect to a particular server be that a Peer in a P2P game or a dedicated server on the net.

The lobby system provides tools for this via the `SetGameServer` method on the lobby

```csharp
public void Lobby.SetGameServer()

public void Lobby.SetGameServer(CSteamID gameServerId)

public void Lobby.SetGameServer(string address, ushort port)

public void Lobby.SetGameServer(string address,
                                ushort port,
                                CSteamID gameServerId)
```

{% hint style="warning" %}
The SetGameServer method can only be called by the "Owner" of the lobby
{% endhint %}

When called Valve will record the information on the Steam Lobby metadata as shown below

![](<../../../.gitbook/assets/image (65).png>)

Each member of the lobby (other than the owner) will be notified by callback which raises the `evtGameServerSet` event located on the lobby and a global version located on the Steamworks Behavior.&#x20;

{% hint style="warning" %}
All members of a lobby should upon joining the lobby register an event handler on the `Lobby.evtGameServerSet` event

```csharp
myLobby.evtGameServerSet.AddListener(HandleGameServerSet);
```

similarly when leaving a lobby each member should remove that handler

```csharp
if(myLobby != null)
    myLobby.evtGameServerSet.RemoveListener(HandleGameServerSet);
```
{% endhint %}
