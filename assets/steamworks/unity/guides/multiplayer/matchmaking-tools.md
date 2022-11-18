---
description: >-
  Understanding what a Steam lobby is and is not, getting started with Steam
  Lobby
---

# Lobby

<figure><img src="../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Steam Matchmaking is driven primarily through the Steam Lobby feature. In a nutshell, the concept is that players will create a "lobby". You can think of this a bit like a chat room. This lobby has "metadata" associated with it which can be used to search for lobbies, filtering the results to just those the player cares about.‌

The metadata concept of Steam Lobby is where most of the functionality comes into play. The owner or "host" of a lobby can set the metadata on a lobby and anyone else can read that data, and the Steam Lobby search system can use that data to refine search results. In addition, each member within a lobby has a set of metadata associated with them. Lobby member metadata can only be set by the member it is related to and can only be read by other members of that lobby.‌

In summary lobby metadata is for stating the intent of the session or the status of the session and is accessible by everyone. Member metadata is for stating the intent of a member or the status of a member and is writable only by that member and readable only by fellow members of the same lobby.‌

You can read more about Steam's Matchmaking system on Valve's developer documentation.

{% embed url="https://partner.steamgames.com/doc/features/multiplayer#matchmaking" %}

## Key Concepts

### Lobby?

The first and most important thing to understand is that a lobby is not a network feature or concept. That is being in a lobby does not require a network connection, a network connection does not require a lobby. Lobby and Networking are two completely independent concepts.&#x20;

Please do not confuse a lobby with anything to do with a network or network connection.

### Types

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

### Members

Every user that has joined the lobby is identified as a [LobbyMember.](../../../objects/lobby-member-data.md) Each member in a lobby has its own set of metadata which all other members can read but only the member its self can set. To clarify that means you can only set your own lobby member metadata but you can read everyones. You cannot however read lobby member metadata if you are not a member of the lobby.

### Metadata

Metadata refers to data stored on the lobby or on a lobby member. Put simply its a collection of key value pairs where the key and value are a simple string. So you can think of it much like a&#x20;

```csharp
Dictionary<string, string>
```

The metadata stored on the lobby can be seen by anyone able to see the lobby and can be used to  filter results when searching for a lobby using Steam's matchmaking system.

In contrast metadata stored on a lobby member can only be seen by members of the lobby and is used only to share for example user configuration.

When metadata is changed the Steam API will raise the lobby data changed event ... that event will indicate what object's data changed by not what data field changed so for example if the event indicates the lobby data changed you should check all the lobby metadata where as if it indicated a members data changed you should check that members metadata.

The event in question is exposed on the Lobby Manager as [evtDataUpdated ](../../components/lobby-manager.md#evtdataupdated)and in the Matchmaking API as [EventLobbyDataUpdate](../../../api/matchmaking.md#eventlobbydataupdate).

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

To learn more check out the [Lobby](../../../objects/lobby-data.md#introduction) and [LobbyMember ](../../../objects/lobby-member-data.md)articles describing the features of the lobby and lobbyMember structures.

### Chat

While the developer facing part of the Steam API calls it a "Lobby" the backend of the system calls it a chat, this is because in reality a "Lobby" is just a chat room. This chat room has its own metadata as noted above and each member within it has its own metadata and you can send and receive messages containing byte\[] data between all members without a network connection. Our [Lobby Chat Director](../../components/lobby-chat-director.md) can help you get started.

## Working with Lobbies

You can work with lobby in one of 3 main ways; they (from lowest level to highest)

### [Raw API](../../../api/matchmaking.md)

All of the functionality of lobby is defined in the [Matchmaking API](../../../api/matchmaking.md). No matter how you choose to work with Steam lobbies, its this API that will actually be doing the real work. Using the Matchmaking API requires that you have a level of understanding of the underlying Steam API but it does still simplify working with the API by making it Unity centric, handling boiler plate concepts such as the callbacks and simplifying common concepts in a Unity manager e.g. UnityEvents and Actions, simpler calls, etc..

### [Lobby object](../../../objects/lobby-data.md)

[Lobby](../../../objects/lobby-data.md) as in the object in Steamworks Complete is a [struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct) which wraps around ulong and CSteamID. Fundamentally it acts as a lobby ID and is [implicitly convertible](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions) between ulong and CSteamID meaning you can pass it along as if it where a ulong value or a CSteamID and you can assign it from a ulong value or a CSteamID. Beyond being a fancy wrapper around ulong it also has accessors and methods that make working with a specific lobby very easy. Using the lobby object you very likely wont need to touch the raw API at all.

### [Lobby Manager](../../components/lobby-manager.md)

As the name suggests [this is a tool for managing a lobby](../../components/lobby-manager.md). The lobby manager is the easiest way to manage a lobby and is a [Unity component](https://docs.unity3d.com/ScriptReference/Component.html) ... that is you can add it to a GameObject and configure it in Unity editor. The [Lobby Manager](../../components/lobby-manager.md) does more than simply expose Matchmaking events to the Unity editor it handles common concepts for you and makes it easier to work with a lobby through designer friendly tools such as Bolt and other visual scripting assets.

## Player Join / Leave

Your first question when managing a lobby is how to know when the user joins or leaves a lobby and what lobby it was that they joined or left. From low level to high here are the notes!

### Matchmaking API

[EventLobbyEnterSuccess](../../../api/matchmaking.md#eventlobbyentersuccess) and [EventLobbyEventFailed ](../../../api/matchmaking.md#eventlobbyenterfailed)are raised when the local user tries and succeeds or fails respectively to enter a lobby. Both events return the [LobbyEnter\_t ](https://partner.steamgames.com/doc/api/ISteamMatchmaking#LobbyEnter\_t)structure provided by Steam API.

#### Success

```csharp
void HandleLobbyEnterSuccess(LobbyEnter_t arg)
{
    Debug.Log("Success lobby join on lobby ID " + arg.m_ulSteamIDLobby);
}
```

#### Failure

```csharp
void HandleLobbyEnterFailed(LobbyEnter_t arg)
{
    Debug.Log("Failed lobby join on lobby ID " + arg.m_ulSteamIDLobby);
}
```

### Lobby

The lobby object Join method takes a callback so for example

```csharp
Lobby lobbyIWantToJoin = lobbyId;
Lobby.Join((result, ioError) =>
    {
        if(!ioError) //Was their an IO error?
        {
            //cast the chat room responce to the enum for easier reading
            var responce = (EChatRoomEnterResponse)result.m_EChatRoomEnterResponse;

            if (responce == EChatRoomEnterResponse.k_EChatRoomEnterResponseSuccess)
                ;//We are in all is well
            else
            {
                //Failed
                if (responce == EChatRoomEnterResponse.k_EChatRoomEnterResponseLimited)
                    ;//Failed because limited account
            }
        }
        else
            //Yes thier was an IO error
    });
```

So we do a bit more work here so we can understand if it was a success or not, and if not why not. The [EChatRoomEnterResponce](https://partner.steamgames.com/doc/api/steam\_api#EChatRoomEnterResponse) tells us why.

{% hint style="info" %}
In our example above we used expression to create an anon method. This is a style choice you can learn more about [expression ](../../../../../company/concepts/development/lambda-expressions.md)and [anon methods](../../../../../company/concepts/development/callbacks.md#callback-examples) in our other articles.
{% endhint %}

### Lobby Manager

Lobby manager makes this supper easy. Using Lobby Manager you don't need to use any code at all if you don't want. You will see right in the inspector a [evtEnterSuccess ](../../components/lobby-manager.md#evtentersuccess)and an [evtEnterFailed ](../../components/lobby-manager.md#evtenterfailed)event. These work just like the ones on Matchmaking API but of course are accessible from the Unity Editor and only raise for lobbies that where joined through this Lobby Manager.

The fact that Lobby Manager filters its events to only the events that where ran through it makes it much easier when driving UI elements. Most games will have 2 lobbies, 1 for the session aka "matchmaking" and 1 as a player friend group or party. The Matchmaking API events raise for any event on any lobby that the local user is a member of so if a user is in a session lobby and a party lobby the events will raise for both leaving it up to you to sort out which lobby the event goes to.

Lobby Manager only handles events for the lobby that it is "managing" so its filtering the events down for you. Thus when the "evtEnterSuccess" triggers on your MatchmakingObject's LobbyManagaer component you know its related to the matchmaking lobby.

{% hint style="info" %}
Yes you can of course use the Lobby Manager from code as much or as little as you would like. Doing so is no different than using any other Unity component from code.
{% endhint %}

## Others Join / Leave

This is how do you know when some other player joins or leaves the lobby that your in. In other words how do you know when new "peers" come in or go out of the lobby.

### Matchmaking API

This is actually handled via the [EventLobbyChatUpdate ](../../../api/matchmaking.md#eventlobbychatupdate)event which is raised any time a chat event occurs ... including when members join or leave.

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

### Lobby object

Their is no way to do this from the lobby object as the lobby object is a struct and doesn't define events.&#x20;

### Lobby Manager

As always the Lobby Manager makes it easier not just by filtering on the lobby for you but also by splitting the event into two. [evtUserJoined ](../../components/lobby-manager.md#evtuserjoined)and [evtUserLeft ](../../components/lobby-manager.md#evtuserleft)invoke when someone joins or leaves respectively. These events are [UserData ](../../../objects/user-data.md)events meaning they hand you the [UserData ](../../../objects/user-data.md)of the member that joined or left.

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

## Metadata Change

You often need to know when data on the lobby or a given member has changed.

### Matchmaking API

The [EventLobbyDataUpdate ](../../../api/matchmaking.md#eventlobbydataupdate)event is raised when any sort of data is updated for the lobby or a member.

```csharp
void HandleDataChanged(LobbyDataUpdate_t dataUpdated)
{
    //Is this a lobby we care about?
    if(dataUpdated.m_ulSteamIDLobby == Lobby)
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
}
```

### Lobby object

This cannot be done from the Lobby object alone as its an event and the struct doesn't have any of the events.

### Lobby Manager

Lobby manager is much like the Matchmaking API for this one and uses the [evtDataUpdated](../../components/lobby-manager.md#evtdataupdated) method to know when any kind of data has changed.

```csharp
void HandleDataChanged(LobbyDataUpdate_t dataUpdated)
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

## Lobby Data

Writing lobby metadata data can only be done by the owner of the lobby. Metadata on the lobby is what is used when searching for a lobby and is what you would use to express configuration and settings of the session the lobby deals with. For example if you wanted to let all users know what map the session will be on then you would set a lobby metadata data field map = X.&#x20;

### Matchmaking API

Use the [SetLobbyData](../../../api/matchmaking.md#setlobbydata) method to apply lobby data. This can only be done if the user is the owner of the lobby.

```csharp
if(Matchmaking.Client.SetlobbyData(lobby, key, value))
    ;//Steam took the request
else
    ;//Steam said no, your probably not the owner.
```

### Lobby

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
// Is the same as
myLobby["z_heathenReady"] = "true";

//IsGroup
myLobby.IsGroup = true;
// Is the same as
myLobby.SetType(ELobbyType.k_ELobbyTypeInvisbile);
myLobby["z_heathenMode"] = "Group";
```

### Lobby Manager

The lobby manager lets you use both approaches

```csharp
lobbyManager.SetLobbyData(key, value);
// or
var lobby = lobbyMannager.Lobby;
lobby["key"] = "value";
```

## General Use Cases

### Authenticate Users

{% hint style="warning" %}
Steam Authentication is not used to prove a person is who they say they are. Steam API already does that implicitly so you know if you see them and can be in a lobby with them, then they are in fact who they say they are and do in fact own a license to this app ID.\
\
Steam Authentication is used to establish trust between users and other users or between users and Steam Game Servers. In particular it can be used to validate the contents of Steam Inventory and it can be used to check the VAC status of the user in question.
{% endhint %}

First you need to understand what Steam Authentication is and is not and how it works in general. Please read the Steam Authentication article for more information on that. As to how you can use it with lobby.

The Lobby Chat system can send and receive byte\[] data thus you can send Authentication ticket data over the Lobby Chat system. In most cases we recommend you create a LobbyChatMessage struct for your self so you can know what kind of message has been sent.

```csharp
[Serializable]
public struct CustomChatMessage
{
    public enum Type
    {
        TextMessage,
        AuthenticationTicket
    }
    
    public Type type;
    public byte[] data;
    public string message;
}
```

With something like the above you could then send the message as

```csharp
Authentication.GetAuthSessionTicket((ticket, IOError) =>
{
    if(!IOError)
    {
        var message = new CustomChatMessage
        {
            type = CustomChatMessage.Type.AuthenticationTicket,
            data = ticket.data
        };
        lobbyChatDirector.Send(message);
    }
});
```

This would generate an auth ticket and when done it would send that auth ticket over the lobby chat director. You should handle receiving a chat message in a similar manner.

First make sure you are listening to the message received event

```csharp
void Start()
{
    lobbyChatDirector.evtMessageRecieved.AddListener(HandleChatMessage);
}
```

Then in that handler you need to work with the message received

```csharp
void HandleChatMessage(LobbyChatMsg message)
{
    var customChatMessage = message.FromJson<CustomChatMessage>();
    if(customChatMessage.type == CustomChatMessage.Type.AuthenticationTicket)
    {
        //Only the user is the owner do we bother with auth
        if(lobbyManager.IsPlayerOwner)
        {
            var responce = Authentication.BeginAuthSession(
                customChatMessage.data, 
                message.sender, 
                result =>
                {
                    //... handle the result
                }
        }
    }
}
```

You can learn more about handling the result of a `BeginAuthSession` in our article on [Steam Authentication](../authentication.md#begin-auth-session).

### Create a Lobby or Group.

For more information on lobby types see Valve's documentation [https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs](https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs)&#x20;

See the [API.Matchmaking](../../../api/matchmaking.md#create-lobby) interface for details on creating a lobby. In addition the [Lobby Manager](../../components/lobby-manager.md) tools can help you create, join and manage a lobby for a specific function in your game.&#x20;

Lets say for example you use 2 types of lobbies in your game

*   Party

    This would be where you have your player gather a group of friends together to play together i.e. a group or party as seen in MMOs, MOBA or really any game with a coop feature
*   Session Lobby

    This would be where you have your player's configure a game play session and wait for competitors to join or similar. This is the most typical use of a lobby and what drives matchmaking in your game.

In the above use case you would attack a [Lobby Manager](../../components/lobby-manager.md) to your Party UI and another to your Session UI. You would configure each accordingly and each can manage its own chat and metadata features. This helps you split functionality across concepts unique to your game.

### Find and Join Lobbies

The easiest way to search for and join lobbies is through the [Lobby Manager](../../components/lobby-manager.md) tool. Alternatively you can use Heathen's API.Matchmaking directly to easily search for and join lobbies.&#x20;

Aside from browsing for a lobby you can handle invite and joining of lobby invites. Inviting a friends to lobby can be done in a number of ways including from outside of your game via the Steam Friends list.

Internally to you game you can use the [User Data](../../../objects/user-data.md) object to invite a specific player. You would have access to this object from various tools and interfaces including [Friends](../../../api/friends.md), [Clans ](../../../api/clans.md)and there related chat systems. When you send an invite it is up to that user to accept it and there are multiple use cases for how they might accept the invite

#### While In game

In this case the accepting user is already in game and so the Game Lobby Join Invite event will be raised on the [Overlay Manger](../../components/overlay-manager.md#events) and its related [API.Overlay](../../../api/overlay.md#game-lobby-join-requested) interface.

#### While out of game

In this case the accepting user is not yet in game and so the Steam client will launch the game and pass as an argument on the command line the lobby connection information. It is up to you to handle this argument, navigate to the appropriate place in your game e.g. the lobby UI and then join the lobby ID indicated on that argument.

A crude example follows

```csharp
Lobby targetLobby = CommandLine.GetSteamLobbyInvite();
if(targetLobby.IsValid)
{
    //We should probably navigate to the proper place in game first
    targetLobby.Join((result, error) =>
    {
        if(!error)
            Debug.Log("We have joined the lobby");
    });
}
```

### Reading Lobby Data

You can read the metadata of a lobby you have queried for or are a member of without issue. If you wanted to read the data on a lobby you had been invited to its best to join that lobby first.

{% hint style="info" %}
If you get the lobby join requested event or if you see the lobby invite ID on the command line then you know the user has already "accepted" the invite and you should join said lobby.\
\
Thus its best to join the lobby and then read its data as a member.
{% endhint %}

In the rare case you need to read the data before you join you would first have to [Request the data](../../../api/matchmaking.md#requestlobbydata) and wait for the [EventLobbyDataUpdate](../../../api/matchmaking.md#eventlobbydataupdate) event to trigger indicated the data had been downloaded.

### Using Lobby Chat

Steam's Lobby system includes a simple chat system able to handle text or data. The easiest way to interact with lobby chat is via the [Lobby Chat Director](../../components/lobby-chat-director.md) which needs to be added to the same object as your [Lobby Manager](../../components/lobby-manager.md).

You can also interact with lobby chat manually through the [API.Matchmaking](../../../api/matchmaking.md) interface.

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

![](<../../../../../.gitbook/assets/image (65).png>)

Each member of the lobby (other than the owner) will be notified by callback which raises the `EventLobbyGameCreated` event located on the [API.Matchmaking](../../../api/matchmaking.md) interface and exposed through the [Lobby Manager](../../components/lobby-manager.md).&#x20;

{% hint style="warning" %}
All members of a lobby should upon joining the lobby register an event handler on the `Lobby.evtGameServerSet` event

```csharp
API.Matchmaking.Client.EventLobbyGameCreated.AddListener(HandleGameServerSet);
```
{% endhint %}

##
