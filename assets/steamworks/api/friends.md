---
description: Access rich presence, user data and more through the Friends interface
---

# Friends

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

```csharp
using API = HeathenEngineering.SteamworksIntegraiton.API;
```

```csharp
public static class API.Friends
```

The whole of the friends system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Friends.Client
```

### What can it do?

You can list the clan owner, its officers, open the clan chat in overlay or join the clan's chat in game. The most common use game developers look for and the most complex is to join the clan chat in game.

### Related Componenets

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/friend-manager" %}

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/user-data" %}

## Events

The following events are available on this interface, events are exposed for each of the availabel "callbacks" in the Steam API for the underlying Steam interface.

### Game Connected Friend Chat Msg

Called when chat message has been received from a friend.

{% hint style="info" %}
See the [Chatting](friends.md#chatting) topic for more details.
{% endhint %}

```csharp
API.Friends.Client.EventGameConnectedFriendChatMsg.AddListener(HandleMsg);
```

#### Example Listener

```csharp
private void HandleMsg(UserData sender, string message, EChatEntryType type)
{
    Debug.Log(sender.Name + " sent a message: " + message);
}
```

### Friend Rich Presence Update

Called when Rich Presence data has been updated for a user, this can happen automatically when friends in the same game update their rich presence, or after a call to [Request User Information](friends.md#requesting-user-information).

```csharp
API.Friends.Client.EventFriendRichPresenceUpdate.AddListener(HandleUpdate);
```

#### Example Listener

```csharp
private void HandleUpdate(FriendRichPresenceUpdate_t update)
{
    UserData user = update.m_steamIDFriend;
    Debug.Log(user.Name + " hand an update to there information.");
}
```

### Persona State Change

Called whenever a friends' status changes. This differs from the Friend Rich Presence Update in that it deals with persona information not presence information e.g. avatar image and name primarly.

```csharp
API.Friends.Client.EventPersonaStateChange.AddListener(HandleChange);
```

#### Example Listener

```csharp
private void HandleChange(PersonaStateChange_t change)
{
    UserData user = change.m_ulSteamID;
    Debug.Log(user.Name + " had a change to there information.");
}
```

You can use `change.m_nChangeFlags` to determin what changed about the given user. Note that when Heathen's system detects this event regarding a Persona Change Avatar we automatically create a corisponding Texture2D and assoceate it with the user in question, thus user.Avatar should already be prepared when you recieve this event.

## How To

### Manage Rich Presence

Rich Presence is a powerful social system for full details please read the feature documentiaton linked below

{% embed url="https://partner.steamgames.com/doc/features/enhancedrichpresence" %}

#### Set Rich Presence

You can set the key value data in the user's rich presence

```csharp
API.Friends.Client.SetRichPresence(key, value);
```

#### Clear Rich Presence

You can clear the current rich presence

```csharp
API.Friends.Client.ClearRichPresence();
```

#### Get Rich Presence

You can read rich presence from your local user or any known user.

To get a specific value

```csharp
API.Friends.Client.GetFriendRichPreseence(user, key);
```

Or get the dictionary of all key value pairs

```csharp
API.Friends.Client.GetFriendRichPresnece(user);
```

### Get Friends

It is offten forgot that Steam is a social network. There are multiple groupings of a user's friends that can be read and listed for various uses.

For general use the GetFriends method will return a simple array of UserData representing each friend by its type. This method takes a "flag" representing the type of freind list to return. The options of flags are as follows.

* None
*   Blocked

    The list of blocked users
*   Friendship Requested

    User that have sent a freind invite to the current user
*   Immediate

    The current user's "regular" friends
*   Clan Member

    Users that are in one of the same (small) steam groups/clans as the user
*   On Game Server

    Users that are on the same game server (as set by SetPlayedWith)
*   Requesting Freindship

    Users that the current user has sent a friend invite to
*   Requesting Info

    Users that are currently sending additional info about themselves after a call to RequestUserInformation
*   Ignored

    Users that the current user has ignored from contacting them
*   Ignored Friend

    Users that have ignored the current user; but the current still knows about them
*   Chat Member

    Users in one of the same chats
*   All

    Returns all friend flags

```csharp
var friends = API.Friends.Client.GetFriends(flag);
```

Alternativly friends can be read from a given source. Sources can include groups/clans, chat rooms, lobbies or game servers.

{% hint style="warning" %}
Large Steam groups cannot be iterated by the local user
{% endhint %}

```csharp
var friends = API.Friends.Client.GetFriendsFromSource(sourceId);
```

A second alternative is to get the list of all friends the player has played with recently. This will get friends that the user has previously called SetPlayedWith on.

```csharp
var friends = API.Friends.Client.GetCoplayFriends();
```

If you need to set a given user as a played with friend you can call

```csharp
API.Friends.Client.SetPlayedWith(user);
```

In most cases all of the information you need about a user (or friend) is provided in the UserData returned by these calls. In some cases you may need specific data not accessable through UserData.

#### Get Coplay Game

When you need to know what game the user most recently played with this user.

```csharp
var appId = API.Friends.Client.GetFriendCoplayGame(user);
```

To know when you can check&#x20;

```csharp
var dateTime = API.Friends.Client.GetFriendCoplayTime(user);
```

#### Friend Groups

With the release of the new Friend Chat system Steam gave users the ability to organize there friends into custom groups aka tags. You can query the list of "friend groups" the user has created with&#x20;

```csharp
var groups = API.Friends.Client.GetFriendsGroups();
```

With the groups returned you can fetch the name of the group for display in your UI via&#x20;

```csharp
var groupName = API.Friends.Client.GetFriendsGroupName(group);
```

Once you have the group IDs you can get the list of friends in each group using the group ID provided by GetFriendsGroups.

```csharp
var friends = API.Friends.Client.GetFriendsGroupMembersList(group);
```

### Invite

There are multiple ways to get users to playing together. By using rich presence and the matchmaking system friends can join through the friend system by interacting with the Steam Friends List in Steam UI. This method will cause the game to be launched for that friend with the lobby ID in its command line. If the friend is already in game then the `API.Overlay.Client.EventGameLobbyJoinRequested` event will be raised.

As far as directly inviting a friend to join your game you can use the API.Friends.Client.InviteUserToGame.

```csharp
API.Friends.Client.InviteUserToGame(user, connectionString);
```

When you invite a user in this way if they are not yet in game; when they accept the invite Steam will launch the game with the connection string provided in the commandline. If the user is already in game then the API will raise the `API.Friends.Client.EventGameRichPresenceJoinRequested` event.

Finally you can invite friends to join a specific lobby through the Lobby object its self. This assumes you have your Lobby as priovded by the API.Matchmaking system.

```
lobby.InviteUserToLobby(user);
```

### Chatting

Its possible to handle friend chat in game via the Friends API. To get started you must enable the listen for friends messages

```
API.Friends.Client.ListenForFriendsMessages = true;
```

Setting this value to value will disable the system, this can be enabled and disabled at will.

Once enabled the API.Friends.Client.EventGameConnectedFriendChatMsg event will be raised any time a new message is recieved. The event will contain information about the message which can be used to present the message to a Chat UI.

Example Chat Message Handler

```csharp
private void HandleFriendChatMsg(UserData sender, 
                                 string message,
                                 EChatEntryType type)
{
   // sender is the user that sent the message
   // message is the message string its self
   // type represents the type of message
}
```

To send a responce to a given player e.g. to send a chat message your self use

```
API.Friends.Client.ReplyToFriendMessage(user, message);
```

### Set Persona Name

```
API.Friends.Client.SetPersonaName(name, callback);
```

### Get Persona State

You can get the persona state for the local users via

{% hint style="info" %}
UserData objects can be used to fetch persona state, name and other information typically in a simpler mathod than using the Friends interface directly.
{% endhint %}

```csharp
var state = API.Friends.Client.PersonaState;
```

and to get the persona state for any other user you can use

```csharp
var state = API.Friends.Client.GetFriendPersonaState(user);
```

### Requesting User Information

In most cases this is not nessisary, Steam will generally already have the information for users that the local user "knows" including:

* Freinds
* Members of shared lobbies
* Members of shared game servers
* Members of shared clans/groups (some limitations on large groups)

The use of requesting user information is when retrieving data for user's that the local user does not know off hand.

```csharp
if(API.Friends.Client.RequestUserInformation(user, nameOnly))
    Debug.Log("The request is working");
else
    Debug.Log("We already have this user's information");
```

If the method returns true that indicates that the request is accepted and processing. When it comletes the `API.Friends.Client.EventPersonaStateChange` event will be raised at that time most persona related features will work for this user such as fetching its avatar, name, etc.

{% hint style="warning" %}
Steam is a secure social network, users may chose to hide or block some or all details from some or all people. It is possible that your local user doesn't have rights to another user's name, avatar, etc.



No amount of requesting user information will allow you to query information about a user that is not sharing that information.
{% endhint %}
