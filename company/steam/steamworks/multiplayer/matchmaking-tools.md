---
description: >-
  Understanding what a Steam lobby is and is not, getting started with Steam
  Lobby
---

# 🛋️ Lobby

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
While Steam Lobby is not a true multiplayer feature ... it is in reality nothing but a chat room with metadata ... even called "Chat" on Valve's backend.\
\
It is nonetheless most commonly used for player parties and session matchmaking for we have listed it under the Multiplayer guides section.
{% endhint %}

Steam Matchmaking is driven primarily through the Steam Lobby feature. In a nutshell, the concept is that players will create a "lobby". You can think of this a bit like a chat room. This lobby has "metadata" associated with it which can be used to search for lobbies, filtering the results to just those the player cares about.‌

The metadata concept of Steam Lobby is where most of the functionality comes into play. The owner or "host" of a lobby can set the metadata on a lobby and anyone else can read that data, and the Steam Lobby search system can use that data to refine search results. In addition, each member within a lobby has a set of metadata associated with them. Lobby member metadata can only be set by the member it is related to and can only be read by other members of that lobby.‌

In summary lobby metadata is for stating the intent of the session or the status of the session and is accessible by everyone. Member metadata is for stating the intent of a member or the status of a member and is writable only by that member and readable only by fellow members of the same lobby.‌

You can read more about Steam's Matchmaking system in Valve's developer documentation.

{% embed url="https://partner.steamgames.com/doc/features/multiplayer#matchmaking" %}

## Key Concepts

### Lobby?

The first and most important thing to understand is that a lobby is not a network feature or concept. That is being in a lobby does not require a network connection, a network connection does not require a lobby. Lobby and Networking are two completely independent concepts.&#x20;

Please do not confuse a lobby with anything to do with a network or network connection.

### Types

The following explains; as clearly as Steam documentation allows, the available lobby types and when and how you might use them.

*   Private

    Classified as a "Normal" lobby by Steam.

    The only way to join a private lobby is to be invited to it via the Lobby.InvitePlayer feature. This can be useful in coop games when your player wants to play with a specific friend but doesn't want to be bothered by requests to join or public searches.

    This lobby will not appear in searches, it will not appear on the user's friends list or rich presence data.
*   Friends Only

    Classified as a "Normal" lobby by Steam.

    This lobby can only be joined by friends of the owner or by people directly invited to it. This lobby does appear on the user's friends list but does not appear in lobby lists or searches. This is useful when the player wants friends to be able to drop in / out but doesn't want to be bothered by random players.
*   Public

    Classified as a "Normal" lobby by Steam.

    This is the typical lobby you will see used in most games. It's the classic "Matchmaking" lobby that appears on the user's friends list and can be searched for and joined by any matching player.
*   Invisible

    This is the lobby type that Valve/Steam allows a user to be a member of 2 of this type.&#x20;

    This lobby is not visible in the friends list but can be searched for. That might be confusing at first read.

    A random user can search for this lobby as you would a public lobby but this lobby will not show up on the Steam Friends list hence "invisible"

### Members

Every user that has joined the lobby is identified as a [LobbyMember.](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-member-data.md) Each member in a lobby has its own set of metadata which all other members can read but only the member itself can set. To clarify that means you can only set your lobby member metadata but you can read everyone else's data. You cannot however read lobby member metadata if you are not a member of the lobby.

### Metadata

Metadata refers to data stored in the lobby or on a lobby member. Put simply it's a collection of key-value pairs where the key and value are a simple string. So you can think of it much like a&#x20;

```csharp
Dictionary<string, string>
```

The metadata stored on the lobby can be seen by anyone able to see the lobby and can be used to filter results when searching for a lobby using Steam's matchmaking system.

In contrast, metadata stored on a lobby member can only be seen by members of the lobby and is used only to share for example user configuration.

When metadata is changed the Steam API will raise the lobby data changed event ... that event will indicate what object's data changed not what data field changed so for example if the event indicates the lobby data changed you should check all the lobby metadata whereas if it indicated a members data changed you should check that members metadata.

The event in question is exposed on the Lobby Manager as [evtDataUpdated ](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md#evtdataupdated)and in the Matchmaking API as [EventLobbyDataUpdate](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#eventlobbydataupdate).

As far as setting metadata you can use the indexers to set metadata for example if you have a `Lobby` in memory such as from the lobby manager.

```csharp
var lobby = lobbyManager.Lobby;
```

Then you can set a metadata field on it such as

```csharp
lobby["thisField"] = "thisValue";
```

Similarly if you have a `LobbyMember` in memory you can do the same thus

```csharp
var member = lobby.Me;
member["thisField"] = "thisValue";
```

To learn more check out the [Lobby](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-data.md#introduction) and [LobbyMember ](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-member-data.md)articles describing the features of the lobby and lobbyMember structures.

### Chat

While the developer-facing part of the Steam API calls it a "Lobby" the backend developer-facing calls it a chat, this is because in reality a "Lobby" is just a chat room. This chat room has its own metadata as noted above and each member within it has its own metadata and you can send and receive messages containing byte\[] data between all members without a network connection. Our [Lobby Chat Director](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-chat-director.md) can help you get started.

### Invite to Lobby

You can invite friends to join a lobby you are a member of This works rather or not the friend is currently in the game. The general workflow for this process is

{% hint style="warning" %}
When User B clicks "Accept" \
That DOES NOT join User B to the lobby\
\
That simply notifies the game that User B has indicated they would like to join that lobby. \
\
It is up to you as a game developer to handle that event appropreatly for your game. Understand that the player could already be in a lobby, they could already be in a match, they could be in the process of exiting. The user that invited them might have invited a ton of other users and now the lobby is full, the user might have clicked Accept hours after the invite was sent ... there are SO MANY reasons why you do not just blindly join the lobby when you get that event.
{% endhint %}

#### Workflow

#### The user is currently In-Game

1. User A joins or creates a lobby
2. User A Invites User B to join the lobby
3. User B clicks the Accept button in the Steam Friends Chat panel (overlay)
4. Your game client invokes the GameLobbyJoinRequest event
5. Your game client handles the event validating the lobby and navigating to the appropriate location in the game
6. Your game client joins the indicated lobby

#### The user is not In-game but does own it

1. User A joins or creates a lobby
2. User A Invites User B to join the lobby
3. User B's clicks the Accept button in the Steam Friends Chat panel (overlay)
4. Steam launches the game passing the Lobby ID in on the command line
5. Your [bootstrap scene](../../../design/bootstrap-scene.md) loads first and is the place to detect command line arguments such as lobby ID.
6. Your game client handles the event validating the lobby and navigating to the appropriate location in the game
7. Your game client joins the indicated lobby

{% hint style="info" %}
When the user has accepted a lobby invite the ID of the lobby will be made available to them but the lobby's data will not be updated in the local cash.

\
You should Request Lobby Data for the invited lobby before attempting to read any of its metadata. You can join the lobby without reading the data however if you are properly validating the lobby you will need to read its data before joining.
{% endhint %}

## Unity Examples

### Getting Started

Bobsi has a quick setup tutorial that goes through a basic simple setup using Heathen's Toolkit for Steamworks. The Working with Lobbies entry below goes into more details and other options you have available.

{% embed url="https://www.youtube.com/watch?v=VBmm0L1Iaqg" %}

### Working with Lobbies

You can work with Lobby in one of 3 main ways; (from lowest level to highest)

#### [Raw API](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md)

All of the functionality of lobby is defined in the [Matchmaking API](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md). No matter how you choose to work with Steam lobbies, it's this API that will be doing the real work. Using the Matchmaking API requires that you have a level of understanding of the underlying Steam API but it does still simplify working with the API by making it Unity-centric, handling boilerplate concepts such as the callbacks and simplifying common concepts in a Unity manager e.g. UnityEvents and Actions, simpler calls, etc..

#### [LobbyData object](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-data.md)

[LobbyData](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-data.md) as in the object in Steamworks Complete is a [struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct) which wraps around ulong and CSteamID. Fundamentally it acts as a lobby ID and is [implicitly convertible](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions) between ulong and CSteamID meaning you can pass it along as if it were a ulong value or a CSteamID and you can assign it from a ulong value or a CSteamID. Beyond being a fancy wrapper around ulong it also has accessors and methods that make working with a specific lobby very easy. Using the lobby object you very likely won't need to touch the raw API at all.

#### [Lobby Manager](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md)

As the name suggests [this is a tool for managing a lobby](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md). The lobby manager is the easiest way to manage a lobby and is a [Unity component](https://docs.unity3d.com/ScriptReference/Component.html) ... that is you can add it to a GameObject and configure it in Unity editor. The [Lobby Manager](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md) does more than simply expose Matchmaking events to the Unity editor it handles common concepts for you and makes it easier to work with a lobby through designer-friendly tools such as Bolt and other visual scripting assets.

### Player Join / Leave

Your first question when managing a lobby is how to know when the user joins or leaves a lobby and what lobby it was that they joined or left. From low level to high here are the notes!

#### Matchmaking API

[EventLobbyEnterSuccess](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#eventlobbyentersuccess) and [EventLobbyEventFailed ](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#eventlobbyenterfailed)are raised when the local user tries and succeeds or fails respectively to enter a lobby. Both events return the LobbyEnter structure provided by Steam API.

#### Success

```csharp
void HandleLobbyEnterSuccess(LobbyEnter arg)
{
    Debug.Log("Success lobby join on lobby ID " + arg.m_ulSteamIDLobby);
}
```

#### Failure

```csharp
void HandleLobbyEnterFailed(LobbyEnter arg)
{
    Debug.Log("Failed lobby join on lobby ID " + arg.m_ulSteamIDLobby);
}
```

#### Lobby

The lobby object Join method takes a callback so for example

```csharp
LobbyData lobbyIWantToJoin = lobbyId;
lobbyIWantToJoin.Join((result, ioError) =>
    {
        if(!ioError) //Was their an IO error?
        {
            if (result.Response == EChatRoomEnterResponse.k_EChatRoomEnterResponseSuccess)
                ;//We are in all is well
            else
            {
                //Failed
                if (result.Response == EChatRoomEnterResponse.k_EChatRoomEnterResponseLimited)
                    ;//Failed because of a limited account
            }
        }
        else
            //Yes there was an IO error
    });
```

So we do a bit more work here so we can understand if it was a success or not, and if not why not. The [EChatRoomEnterResponce](https://partner.steamgames.com/doc/api/steam\_api#EChatRoomEnterResponse) tells us why.

{% hint style="info" %}
In our example above we used expression to create an anon method. This is a style choice you can learn more about [expression ](../../../development/lambda-expressions.md)and [anon methods](../../../development/callbacks.md#callback-examples) in our other articles.
{% endhint %}

#### Lobby Manager

Lobby manager makes this super easy. Using Lobby Manager you don't need to use any code at all if you don't want. You will see right in the inspector an [evtEnterSuccess ](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md#evtentersuccess)and an [evtEnterFailed ](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md#evtenterfailed)event. These work just like the ones on Matchmaking API but of course are accessible from the Unity Editor and only raise for lobbies that were joined through this Lobby Manager.

The fact that Lobby Manager filters its events to only the events that were run through it makes it much easier when driving UI elements. Most games will have 2 lobbies, 1 for the session aka "matchmaking" and 1 for a player friend group or party. The Matchmaking API events raise for any event on any lobby that the local user is a member of so if a user is in a session lobby and a party lobby the events will raise for both leaving it up to you to sort out which lobby the event goes to.

Lobby Manager only handles events for the lobby that it is "managing" so it is filtering the events down for you. Thus when the "evtEnterSuccess" triggers on your MatchmakingObject's LobbyManagaer component you know it's related to the matchmaking lobby.

{% hint style="info" %}
Yes, you can of course use the Lobby Manager from code as much or as little as you would like. Doing so is no different than using any other Unity component from code.
{% endhint %}

### Others Join / Leave

This is how do you know when some other player joins or leaves the lobby that your in. In other words, how do you know when new "peers" come in or go out of the lobby?

{% embed url="https://www.youtube.com/watch?v=uJ4fEPy9XQ8" %}

#### Matchmaking API

This is actually handled via the [EventLobbyChatUpdate ](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#eventlobbychatupdate)event which is raised any time a chat event occurs ... including when members join or leave.

The handler for this event would look something like this, note the work is done in the [EChatMemberStateChange](https://partner.steamgames.com/doc/api/ISteamMatchmaking#EChatMemberStateChange) data

```csharp
void HandleChatUpdate(LobbyChatUpdate_t arg)
{
    //Check if this is for the lobby we care about
    if(arg.m_ulSteamIDLobby == Lobby)
    {
        //Cast the chat member state to an enum for easy reading
        var state = (EChatMemberStateChange)arg.m_rgfChatMemberStateChange;
        if (state == EChatMemberStateChange.k_EChatMemberStateChangeEntered)
            ;//arg.m_ulSteamIDUserChanged joined
        else
            ;//arg.m_ulSteamIDUserChanged left us
    }
}
```

#### Lobby object

There is no way to do this from the lobby object as the lobby object is a struct and doesn't define events.&#x20;

#### Lobby Manager

As always the Lobby Manager makes it easier not just by filtering on the lobby for you but also by splitting the event into two. [evtUserJoined ](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md#evtuserjoined)and [evtUserLeft ](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md#evtuserleft)invoke when someone joins or leaves respectively. These events are [UserData ](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/user-data.md)events meaning they hand you the [UserData ](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/user-data.md)of the member that joined or left.

```csharp
void HandleUserJoined(UserData arg)
{
    //arg is the user that joined us
}
```

```csharp
void HandleUserLeft(UserData arg)
{
    //arg is the user that left us
}
```

### Invited to Lobby

[Request Lobby Data](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#requestlobbydata)

Gets data about a lobby, if you have been invited to a lobby you will probably want to get data about it before attempting to join it. This can be useful when preparing the lobby UI or to confirm that the lobby is a valid lobby for the local player.

#### Game Lobby Join Requested Event

This is the event that Valve's Steam will invoke when the user is currently in your game and accepts an invite to a lobby for your game. The event can be found on the [Overlay.Client](../../../../toolkit-for-steamworks-sdk/unity/api/overlay.client.md#event-game-lobby-join-requested) and on the [Overlay Manager](../../../../toolkit-for-steamworks-sdk/unity/components/overlay-manager.md#evtgamelobbyjoinrequested).

#### Command Arguments

In the event the user accepts an invite to a lobby in your game and is not currently playing your game then Steam will launch your game with the lobby ID on the command line. We have provided you with tools to make detecting this easy.

#### Steamworks Behaviour

Our Steamworks Behaviour script checks for this case on initialization and raises an event if found.

#### CommandLine

CommandLine is a tool available in the HeathenEngineering namespace. It can read common command line arguments for you including a Steam Lobby ID.

```csharp
LobbyData targetLobby = CommandLine.GetSteamLobbyInvite();
if (targetLobby.IsValid)
{
    //Launched as a result of accepting a lobby invite
    //targetLobby is the lobby ID the user wants to join
}
```

### Metadata

You often need to know when data on the lobby or a given member has changed.

#### Matchmaking API

The [EventLobbyDataUpdate ](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#eventlobbydataupdate)event is raised when any sort of data is updated for the lobby or a member.

```csharp
void HandleDataChanged(LobbyDataUpdateEventData dataUpdated)
{
    //Is this a lobby we care about?
    if(dataUpdated.lobby == Lobby)
    {
        if(!dataUpdated.member.HasValue)
        {
            //It was lobby data that was updated
        }
        else
        {
            //It was this member that updated
            //dataUpdated.member.Value
        }
    }
}
```

#### Lobby object

This cannot be done from the Lobby object alone as it is an event and the struct doesn't have any of the events.

#### Lobby Manager

Lobby Manager is much like the Matchmaking API for this one and uses the [evtDataUpdated](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md#evtdataupdated) method to know when any kind of data has changed.

```csharp
void HandleDataChanged(LobbyDataUpdateEventData dataUpdated)
{
    //Is this a lobby we care about?
    if(dataUpdated.lobby == Lobby)
    {
        if(!dataUpdated.member.HasValue)
        {
            //It was lobby data that was updated
        }
        else
        {
            //It was this member that updated
            //dataUpdated.member.Value
        }
    }
}
```

Metadata Read/Write

Writing lobby metadata data can only be done by the owner of the lobby. Metadata on the lobby is what is used when searching for a lobby and is what you would use to express configuration and settings of the session the lobby deals with. For example if you wanted to let all users know what map the session will be on then you would set a lobby metadata data field map = X.&#x20;

#### Matchmaking API

Use the [SetLobbyData](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#setlobbydata) method to apply lobby data. This can only be done if the user is the owner of the lobby.

```csharp
if(Matchmaking.Client.SetlobbyData(lobby, key, value))
    ;//Steam took the request
else
    ;//Steam said no, your probably not the owner.
```

#### Lobby Data

Using the lobby object its a step easier and you have a few options

Simple indexer

```csharp
myLobby["key"] = "value";
// or
var theValue = myLobby["key"];
```

and we have exposed several common fields as fields on the struct

```csharp
//Name
myLobby.Name = "New Name"
// Is the same as
myLobby["name"] = "New Name";

//Game Version
myLobby.GameVersion = "v1.24b";
// is the same as
myLobby["z_heathenGameVersion"] = "v1.24b";

//IsReady
myLobby.IsReady = true;
// Is the same as setting heathenReady on your lobby member data
myLobby.Me["z_heathenReady"] = "true";

//IsGroup
myLobby.IsGroup = true;
// Is the same as
myLobby.SetType(ELobbyType.k_ELobbyTypeInvisbile);
myLobby["z_heathenMode"] = "Group";
```

#### Lobby Manager

The lobby manager lets you use both approaches

```csharp
lobbyManager.SetLobbyData(key, value);
// or
var lobby = lobbyMannager.Lobby;
lobby["key"] = "value";
```

### Get the Lobby

We are often asked how do you "get" the lobby your in as in once you joined or created a lobby how to do you get to its [LobbyData ](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-data.md)so you can use it for whatever it is you need to use it for.&#x20;

The answer differs depending on context so here are some common cases.

#### Lobby Manager

or for that matter, [Quick Match Lobby Control](../../../../toolkit-for-steamworks-sdk/unity/ui-components/quick-match-lobby-control.md) or [Party Lobby Control](../../../../toolkit-for-steamworks-sdk/unity/ui-components/party-lobby-control.md) or any similar lobby management tool.

In all cases these tools have a field on them named Lobby that returns the lobby they are managing ... similarly you can set the lobby you want them to manage by writing a value to this field.

```csharp
LobbyData lobby = lobbyManager.Lobby;
```

```csharp
lobbyManager.Lobby = lobby_I_want_you_to_manage;
```

#### Session and Group

If you use our tools we will mark lobby's by their type ... that is we will mark the lobby as the "group" lobby when you use the Party Lobby Control and we will mark it as the "session" lobby when you use the Quick Match Lobby Control. Note you can configure the Lobby Manager to set this for you if using it. And you can set this yourself if your creating lobby manually.

To set this your self after the creation of your lobby call

```csharp
//This is a group aka party lobby
lobby.IsGroup = true;
```

or

```csharp
//This is a session lobby
lobby.IsSession = true;
```

Note there should only be 1 group and 1 session lobby at a time, you can then get these special use case lobbies from anywhere in code

```csharp
if(LobbyData.GroupLobby(out var lobby))
{
    //We have a group and it is lobby
}
else
{
    //We do not have a group lobby
}
```

or

```csharp
if(LobbyData.SessionLobby(out var lobby))
{
    //We have a session and it is lobby
}
else
{
    //We do not have a session
}
```

#### Look for it

Our system tracks every lobby the local user is a member of, a user cannot be a member of more than 3 lobbies and so it's trivial to just iterate over the lobbies they are a member of to choose the one you want.

```csharp
foreach(var lobby in API.Matchmaking.Client.memberOfLobbies)
{
    //Test if the lobby is the right lobby
}
```

or if you prefer Linq (we do)

```csharp
//This is how we get the session lobby for you
var lobby = API.Matchmaking.Client.memberOfLobbies.FirstOrDefault(p => p.IsSession);
if(lobby.IsValid)
{
    //We have a winner
}
else
{
    //No such lobby
}
```

### Create a Lobby

For more information on lobby types see Valve's documentation [https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs](https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs)&#x20;

See the [API.Matchmaking](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md#create-lobby) interface for details on creating a lobby. In addition the [Lobby Manager](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md), tools can help you create, join and manage a lobby for a specific function in your game.&#x20;

Let's say for example you use 2 types of lobbies in your game

*   Party

    This would be where you have your player gather a group of friends together to play together i.e. a group or party as seen in MMOs, MOBA or any game with a coop feature
*   Session Lobby

    This would be where you have your players configure a gameplay session and wait for competitors to join or similar. This is the most typical use of a lobby and what drives matchmaking in your game.

In the above use case, you would attack a [Lobby Manager](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md) to your Party UI and another to your Session UI. You would configure each accordingly and each can manage its own chat and metadata features. This helps you split functionality across concepts unique to your game.

### Find and Join Lobbies

The easiest way to search for and join lobbies is through the [Lobby Manager](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md) tool. Alternatively, you can use Heathen's API.Matchmaking directly to easily search for and join lobbies.&#x20;

Aside from browsing for a lobby you can handle invites and joining of lobby invites. Inviting friends to Lobby can be done in several ways including from outside of your game via the Steam Friends list.

Internally to you're game you can use the [User Data](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/user-data.md) object to invite a specific player. You would have access to this object from various tools and interfaces including [Friends](../../../../toolkit-for-steamworks-sdk/unity/api/friends.client.md), [Clans ](../../../../toolkit-for-steamworks-sdk/unity/api/clans.client.md)and their related chat systems. When you send an invite it is up to that user to accept it and there are multiple use cases for how they might accept the invite

#### While In-game

In this case, the accepting user is already in-game so the Game Lobby Join Invite event will be raised on the [Overlay Manger](../../../../toolkit-for-steamworks-sdk/unity/components/overlay-manager.md#events) and its related [API.Overlay](../../../../toolkit-for-steamworks-sdk/unity/api/overlay.client.md#game-lobby-join-requested) interface.

#### While out of the game

In this case, the accepting user is not yet in the game so the Steam client will launch the game and pass as an argument on the command line the lobby connection information. It is up to you to handle this argument, navigate to the appropriate place in your game e.g. the lobby UI and then join the lobby ID indicated on that argument.

A crude example follows

```csharp
LobbyData targetLobby = CommandLine.GetSteamLobbyInvite();
if(targetLobby.IsValid)
{
    //We should probably navigate to the proper place in-game first
    targetLobby.Join((result, error) =>
    {
        if(!error)
            Debug.Log("We have joined the lobby");
    });
}
```

### Using Lobby Chat

{% embed url="https://www.youtube.com/watch?v=2ZqoOBEvnrQ" %}

Steam's Lobby system includes a simple chat system able to handle text or data. The easiest way to interact with lobby chat is via the [Lobby Chat Director](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-chat-director.md) which needs to be added to the same object as your [Lobby Manager](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md).

You can also interact with lobby chat manually through the [API.Matchmaking](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md) interface.

### Notify "Connect to network"

This will set the Game Server information on the lobby and can be done in a number of ways. You are required to have either a Steam ID (which a UserData is) or an IP and Port or both, when you call the SetGameServer method with no input parameters it will assume the owner of the lobby is the Listen Server.

The typical purpose of a lobby is to gather players and settle on the rules and conditions of the multiplayer session. In most cases, you will at some point want to notify players that they should connect to a particular server be that a Peer in a P2P game or a dedicated server on the net.

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

![](<../../../../.gitbook/assets/image (65).png>)

Each member of the lobby (other than the owner) will be notified by a callback which raises the `EventLobbyGameCreated` event located on the [API.Matchmaking](../../../../toolkit-for-steamworks-sdk/unity/api/matchmaking.client.md) interface and exposed through the [Lobby Manager](../../../../toolkit-for-steamworks-sdk/unity/ui-components/lobby-manager.md).&#x20;

{% hint style="warning" %}
All members of a lobby should upon joining the lobby register an event handler on the `Lobby.evtGameServerSet` event

```csharp
API.Matchmaking.Client.EventLobbyGameCreated.AddListener(HandleGameServerSet);
```
{% endhint %}

### Go from Lobby to Network Session

Hopefully, you have read the above so you understand the fundamentals of a lobby and what features it has including [how to notify the other members when it's time to connect to the network](matchmaking-tools.md#notify-connect-to-network).

So your question then is how do you know when to transition from being in the lobby to starting the network session, and we can't answer that for you. This is entirely up to your game design but here are a couple of common use cases.

#### Lobby Full

In this case, you are simply assuming it is time to play when the lobby gets full e.g.&#x20;

```csharp
if(lobby.Full)
{
    //Time to start the network session
}
```

#### Players Ready

In this case, you were assuming it is time to play when the lobby is full and all players have indicated they are ready. Note this requires you to provide the players with a means to set

```csharp
lobby.IsReady = true;
```

This sets the metadata on that user indicating it is ready to play, we use that in the following test

```csharp
if(lobby.Full && lobby.AllPlayersReady)
{
    //Time to start the network session
}
```

#### Then What?

Once you know when you want to start the network session it's time to ... start the network session ... exactly what you need to do to do that depends on the networking tool you chose to use but here is the usual workflow with the code snippets relevant to Steam lobby.

First, you probably want to set the lobby joinable as false. This will prevent newcomers from joining while you transition players over to the network session. Of course, if your game supports "drop-in/drop-out" you don't want to do this ... use your judgment with regards to your design.

```csharp
lobby.SetJoinable(false);
```

You would then have the owner do whatever it is your networking tool needs you to do to start up the network session. Don't know what that is? consult your networking tool of choice ... it is usually something like loading up the appropriate scene and using the network manager to call StartHost() or similar.

Once the network session is ready you have the owner notify the other members that it's time to connect to the network session.

```csharp
lobby.SetGameServer();
```

Notice in this case we do not provide any parameters to the [SetGameServer ](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-data.md#set-game-server)call ... this is assuming your session will be P2P and that the owner is the host ... for more information please consult the article on [LobbyData](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-data.md).

This will cause the GameServerSet event to be triggered as noted in the [Notify "Connect to network"](matchmaking-tools.md#notify-connect-to-network) entry.

When users see that event they will use the GameServer information in the lobby to know who to connect to. You have options here and which you would use depends again on your game and your design. The following code simply highlights what's available in the [LobbyGameServer ](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-game-server.md)information you read on the [GameServer ](../../../../toolkit-for-steamworks-sdk/unity/classes-and-structs/lobby-data.md#game-server)field of the lobby.

```csharp
//When you are connecting over SteamNetworking/Socket 
//and need the peer ID or a Steam game server ID.
CSteamID steamIdToConnectTo = lobby.GameServer.id;
```

Once your members connect they would typically then leave the lobby ... this is not a requirement simply typical. You do not need the lobby once you have the network session going unless, of course, you're doing the classic "Drop-In/Drop-Out" style gameplay in which case the lobby should persist for the duration of the session.

## Unreal Examples

### Player Join / Leave

A common question asked is how to know the user Joins or Leaves a lobby. A player will not join or leave a lobby if you do not call Join Lobby or Leave Lobby respectively so you define when this will happen.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/join-lobby.md" %}
[join-lobby.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/join-lobby.md)
{% endcontent-ref %}

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/leave-lobby.md" %}
[leave-lobby.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/leave-lobby.md)
{% endcontent-ref %}

### Others Join / Leave

This is how you know when some other player joins or leaves the lobby that you are in. In other words, how do you know when new "peers" come in or go out of the lobby?

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-chat-update.md" %}
[lobby-chat-update.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-chat-update.md)
{% endcontent-ref %}

<figure><img src="../../../../.gitbook/assets/image (374).png" alt=""><figcaption></figcaption></figure>

This event is executed when a user enters or exits. The event tells you the ID of the lobby that was effected, what user it was that was effected, who caused the change if that is different and what change was made.

Note that while "Kicked" is an option for state change that is an internal feature of Steam ... you cannot kick a user out of a lobby at least not with a feature built-in by Valve.

### Invited to Lobby

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/request-lobby-data.md" %}
[request-lobby-data.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/request-lobby-data.md)
{% endcontent-ref %}

When your player is invited to a lobby they will not have a view of that lobby's data which you may want to check before joining such as to validate that the lobby is suitable for the player's current state.&#x20;

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-join-requested.md" %}
[lobby-join-requested.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-join-requested.md)
{% endcontent-ref %}

The Lobby Join Requested event is executed when the user accepts a lobby invite and is currently in-game.&#x20;

Note the player is not automatically joined to the lobby, it's up to you to validate that the lobby is fit for purpose given the user and state of the game. To then navigate to an appropriate place in the game and join the lobby through the normal means of [Join Lobby](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/join-lobby.md).

If the player accepts an invite but is not currently in the game, then Steam will launch the game with the lobby ID passed in on the command line.

<figure><img src="../../../../.gitbook/assets/image (375).png" alt=""><figcaption></figcaption></figure>

Above we are fetching the command line, checking it for the `+connect_lobby` argument and if found we parse that value to an int64 which we can use as a Lobby ID for other operations such as Requesting the Lobby Data or Joining the Lobby.

### Metadata

To detect when metadata has changed on the lobby or a member of the lobby you can use the Lobby Data Update event.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-data-update.md" %}
[lobby-data-update.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-data-update.md)
{% endcontent-ref %}

This event is executed when any data changes on a lobby be it data for the lobby itself or a member of the lobby.

You can get or set data on a player's lobby member using Set Lobby Member Data

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-lobby-member-data.md" %}
[get-lobby-member-data.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-lobby-member-data.md)
{% endcontent-ref %}

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/set-lobby-member-data.md" %}
[set-lobby-member-data.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/set-lobby-member-data.md)
{% endcontent-ref %}

Only the members themselves can set their data but any member of the lobby can read it. This is useful for setting things such as player selection, map votes, etc.

The owner of a lobby can do the same on the lobby itself, the data on a lobby can be used to search for and filter lobbies and can be read by anyone not just members of the lobby.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-lobby-data.md" %}
[get-lobby-data.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-lobby-data.md)
{% endcontent-ref %}

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/set-lobby-data.md" %}
[set-lobby-data.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/set-lobby-data.md)
{% endcontent-ref %}

### Create Lobby

Creating a lobby is a simple function call, once the lobby is created you can then update its data, change its type, mark it as joinable or not, etc.

A lobby is simply an ID, all lobbies will have 1 or more members, you do not "destroy" or "close" a lobby, they simply cease to exist when there are no members in them.

1 user is always said to "own" the lobby, by default, this is the user that created it but that can be changed after e.g. the owner can set a different user as owner.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/create-lobby.md" %}
[create-lobby.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/create-lobby.md)
{% endcontent-ref %}

### Find and Join Lobbies

To find a lobby to join you set up a request by adding filters, then making the request. When you make a request it clears the filters so you will need to set up the filters again to make a subsequent request.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/add-request-lobby-list-filter.md" %}
[add-request-lobby-list-filter.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/add-request-lobby-list-filter.md)
{% endcontent-ref %}

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/request-lobby-list.md" %}
[request-lobby-list.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/request-lobby-list.md)
{% endcontent-ref %}

<figure><img src="../../../../.gitbook/assets/image (378).png" alt=""><figcaption></figcaption></figure>

In the above example, we set up a search to find a lobby where map = Some Cool Map Name

We then iterate over the results and get the Lobby by index for each.

The above is not functional but shows you the important nodes to work with. In functional logic, you would build out a more complete search filter, check the result count was greater than zero, and then handle each result as required.

For example, a quick match would simply join the first lobby found. As the Steam Lobby system is a Matchmaking query the first lobby found is the "best" lobby to join.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/join-lobby.md" %}
[join-lobby.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/join-lobby.md)
{% endcontent-ref %}

### Using Lobby Chat

A Steam Lobby is little more than a fancy chat room, Steam API even refers to a Lobby ID as a CSteamID of type Chat. You can use a lobby as a chat room sending and receiving data messages without needing a network session. Note that this is a chat, so it's not suitable for real-time data such as Voice Streaming but can handle simple text messages or even send serialized data such as authentication tickets.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/send-lobby-chat.md" %}
[send-lobby-chat.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/send-lobby-chat.md)
{% endcontent-ref %}

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-chat-msg.md" %}
[lobby-chat-msg.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-chat-msg.md)
{% endcontent-ref %}

The Lobby Chat Msg event is executed when a chat message is received and can be used with the [Get Lobby Chat Entry](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-lobby-chat-entry.md) node to read the message

<figure><img src="../../../../.gitbook/assets/image (379).png" alt=""><figcaption></figcaption></figure>

### Notify "Connect to network"

Steam provides a built-in way to notify members of a lobby when the network is ready for them to connect. This is done by the owner of the lobby calling Set Game Server or its variants.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/set-lobby-game-server.md" %}
[set-lobby-game-server.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/set-lobby-game-server.md)
{% endcontent-ref %}

This has several variations for Peer to Peer (where the lobby owner is the server), Steam Game Server (where the server is addressed by an ID) as well as traditional IP/Port-based connection addressing.

When the owner of the lobby calls this all members will receive the Lobby Game Created event.

{% content-ref url="../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-game-created.md" %}
[lobby-game-created.md](../../../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/events/lobby-game-created.md)
{% endcontent-ref %}

This event provides the connection details for the server to all members&#x20;

<figure><img src="../../../../.gitbook/assets/image (381).png" alt=""><figcaption></figcaption></figure>
