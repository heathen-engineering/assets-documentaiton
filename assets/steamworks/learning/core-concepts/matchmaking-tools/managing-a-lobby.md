---
description: Lobby events, what's their and how to use it
---

# Managing a Lobby

## Overview

Once you understand what a Steam lobby is ... and most importantly what it is not (it is not a networking features); the next questions are usually around how to work with it. Understanding when the user joins or leaves a lobby, when other members join or leave a lobby, when metadata changes on a lobby or any of the lobby members are all common questions addressed here.

## Options

You can work with lobby in one of 3 main ways; they (from lowest level to highest)

### [Raw API](../../../api/matchmaking.md)

All of the functionality of lobby is defined in the [Matchmaking API](../../../api/matchmaking.md). No matter how you choose to work with Steam lobbies, its this API that will actually be doing the real work. Using the Matchmaking API requires that you have a level of understanding of the underlying Steam API but it does still simplify working with the API by making it Unity centric, handling boiler plate concepts such as the callbacks and simplifying common concepts in a Unity manager e.g. UnityEvents and Actions, simpler calls, etc..

### [Lobby object](../../../objects/lobby.md)

[Lobby](../../../objects/lobby.md) as in the object in Steamworks Complete is a [struct](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/struct) which wraps around ulong and CSteamID. Fundamentally it acts as a lobby ID and is [implicitly convertible](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions) between ulong and CSteamID meaning you can pass it along as if it where a ulong value or a CSteamID and you can assign it from a ulong value or a CSteamID. Beyond being a fancy wrapper around ulong it also has accessors and methods that make working with a specific lobby very easy. Using the lobby object you very likely wont need to touch the raw API at all.

### [Lobby Manager](../../../components/lobby-manager.md)

As the name suggests [this is a tool for managing a lobby](../../../components/lobby-manager.md). The lobby manager is the easiest way to manage a lobby and is a [Unity component](https://docs.unity3d.com/ScriptReference/Component.html) ... that is you can add it to a GameObject and configure it in Unity editor. The [Lobby Manager](../../../components/lobby-manager.md) does more than simply expose Matchmaking events to the Unity editor it handles common concepts for you and makes it easier to work with a lobby through designer friendly tools such as Bolt and other visual scripting assets.

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

Lobby manager makes this supper easy. Using Lobby Manager you don't need to use any code at all if you don't want. You will see right in the inspector a [evtEnterSuccess ](../../../components/lobby-manager.md#evtentersuccess)and an [evtEnterFailed ](../../../components/lobby-manager.md#evtenterfailed)event. These work just like the ones on Matchmaking API but of course are accessible from the Unity Editor and only raise for lobbies that where joined through this Lobby Manager.

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

As always the Lobby Manager makes it easier not just by filtering on the lobby for you but also by splitting the event into two. [evtUserJoined ](../../../components/lobby-manager.md#evtuserjoined)and [evtUserLeft ](../../../components/lobby-manager.md#evtuserleft)invoke when someone joins or leaves respectively. These events are [UserData ](../../../objects/user-data.md)events meaning they hand you the [UserData ](../../../objects/user-data.md)of the member that joined or left.

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

Lobby manager is much like the Matchmaking API for this one and uses the [evtDataUpdated](../../../components/lobby-manager.md#evtdataupdated) method to know when any kind of data has changed.

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
