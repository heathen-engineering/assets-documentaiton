---
description: Access rich presence, user data and more through the Friends interface
---

# Friends.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

```csharp
using FriendsClient = HeathenEngineering.SteamworksIntegration.API.Friends.Client;
```

```csharp
public static class Friends.Client
```

### What can it do?

You can list the clan owner, its officers, open the clan chat in overlay or join the clan's chat in game. The most common use game developers look for and the most complex is to join the clan chat in game.

### Related Componenets

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/friend-manager" %}

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/user-data" %}

## Events

The following events are available on this interface, events are exposed for each of the available "callbacks" in the Steam API for the underlying Steam interface.

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

Called whenever a friends' status changes. This differs from the Friend Rich Presence Update in that it deals with persona information not presence information e.g. avatar image and name primarily.

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

You can use `change.m_nChangeFlags` to determine what changed about the given user. Note that when Heathen's system detects this event regarding a Persona Change Avatar we automatically create a corresponding Texture2D and associate it with the user in question, thus user.Avatar should already be prepared when you receive this event.

## Fields and Attributes

### ListenForFriendsMessages

```csharp
public static bool ListenForFriendsMessages { get; set; }
```

Gets or sets the listen for friends messages. When this is set true you should handle the "Game Connected Friend Chat Msg" event to read incoming messages from friends.

### PersonaName

```csharp
public static string PersonaName => get;
```

Returns the name of the local user.

### PersonaState

```csharp
public static EPErsonaState PErsonaState => get;
```

### Restrictions

```csharp
public static uint Restrictions => get;
```

Checks if the current user is chat restricted, see the link below on the meaning of each value. Any value other than 0 is some sort of restriction.

{% embed url="https://partner.steamgames.com/doc/api/ISteamFriends#EUserRestriction" %}

## Methods

### ClearRichPresence

```csharp
public static void ClearRichPresence()
```

Clears all of the current user's rich presence key/values

### EnumerateFollowingList

```csharp
public static void EnumerateFollowingList(uint index, 
                Action<FriendsEnumerateFollowingList_t, bool> callback)
```

Gets the list of users that the current user is following.

### GetCoplayFriend

```csharp
public static UserData GetCoplayFriend(int coplayFriendIndex)
```

Gets the Steam ID of the recently played with user at the given index.

### GetCoplayFriendCount

```csharp
public static int GetCoplayFriendCount()
```

Gets the number of players that the current user has recently played with, across all games.

### GetCoplayFriends

```csharp
public static UserData[] GetCoplayFriends()
```

Get the list of players the current user has recently played with across all games

### GetFollowerCount

```csharp
public static void GetFollowerCount(UserData userId, 
                Action<FriendsGetFollowerCount_t, bool> callback)
```

Gets the number of users following the specified user.

### GetFriendByIndex

```csharp
public static UserData GetFriendByIndex(int index, EFriendFlags flags)
```

Gets the Steam ID of the user at the given index.

### GetFriendCoplayGame

```csharp
public static AppId_t GetFriendCoplayGame(UserData userId)
```

Gets the app ID of the game that user played with someone on their recently-played-with list.

### GetFriendCoplayTime

```csharp
public static DateTime GetFriendCoplayTime(UserData userId)
```

Gets the timestamp of when the user played with someone on their recently-played-with list.

### GetFriendCount

```csharp
public static int GetFriendCount(EFriendFlags flags)
```

Gets the number of users the client knows about who meet a specified criteria. (Friends, blocked, users on the same server, etc)

### GetFriends

```csharp
public static UserData[] GetFriends(EFriendFlags flags)
```

Returns the users the client knows about who meet the specified criteria.

### GetFriendCountFromSource

```csharp
public static int GetFriendCountFromSource(CSteamID source)
```

Get the number of users in a source (Steam group, chat room, lobby, or game server).

### GetFriendFromSourceByIndex

```csharp
public static UserData GetFriendFromSourceByIndex(CSteamID source, int index)
```

Gets the Steam ID at the given index from a source (Steam group, chat room, lobby, or game server).

### GetFriendsFromSource

```csharp
public static UserData[] GetFriendsFromSource(CSteamID source)
```

Gets the list of friends the user knows from the given source

### GetFriendGamePlayed

```csharp
public static bool GetFriendGamePlayed(UserData userId, 
                                out FriendGameInfo_t results)
```

Checks if the specified friend is in a game, and gets info about the game if they are.

### GetFriendMessage

```csharp
public static string GetFriendMessage(UserData userId, 
                                int index, 
                                out EChatEntryType type)
```

Gets the data from a Steam friends message.

### GetFriendPersonaName

```csharp
public static string GetFriendPersonaName(UserData userId)
```

You really shouldn't need to use this as its the same as simply reading userId.Name however it is maintained to be compatible with Steamworks.NET sample code.

### GetFriendPersonaNameHistory

```csharp
public static string GetFriendPersonaNameHistory(UserData userId, int index)
```

Gets one of the previous display names for the specified user.

```csharp
public static string[] GetFriendPersonaNameHistory(UserData userId)
```

Gets a collection of names the local user knows for the indicated user

### GetFriendPersonaState

```csharp
public static EPersonaState GetFriendPersonaState(UserData userId)
```

Gets the current status of the specified user.

### GetFriendRichPresence

```csharp
public static string GetFriendRichPresence(UserData userId, string key)
```

Get a Rich Presence value from a specified friend.

### GetFriendRichPresenceKeyByIndex

```csharp
public static string GetFriendRichPresenceKeyByIndex(UserData userId, int index)
```

Get the key value of a rich presence field based on its index

### GetFriendRichPresenceKeyCount

```csharp
public static int GetFriendRichPresenceKeyCount(UserData userId)
```

Gets the number of Rich Presence keys that are set on the specified user.

### GetFriendRichPresence

```csharp
public static Dictionary<string, string> GetFriendRichPresence(UserData userId)
```

Gets a collection of the target users rich presence data

### GetFriendsGroupCount

```csharp
public static int GetFriendsGroupCount()
```

Gets the number of friends groups (tags) the user has created.

### GetFriendsGroupIDByIndex

```csharp
public static FriendsGroupID_t GetFriendsGroupIDByIndex(int index)
```

Gets the friends group ID for the given index.

### GetFriendsGroups

```csharp
public static FriendsGroupID_t[] GetFriendsGroups()
```

Gets the number of friends groups (tags) the user has created.

### GetFriendsGroupMembersList

```csharp
public static CSteamID[] GetFriendsGroupMembersList(FriendsGroupID_t groupId)
```

Returns the Steam IDs of the friends

### GetFrinedsGroupName

```csharp
public static string GetFriendsGroupName(FriendsGroupID_t groupId)
```

Gets the name for the given friends group.

### GetFriendSteamLevel

```csharp
public static int GetFriendSteamLevel(UserData userId)
```

Gets the level of the indicated user if kown by the local user

### GetFriendAvatar

```csharp
public static void GetFriendAvatar(UserData userId, Action<Texture2D> callback)
```

This can be performed from the [UserData](../data-layer/user-data.md) object directly. It simply requests and load's the user's avatar into a Unity Texture2D. This will not duplicate memory it will used existing loaded data for the image if present.

### UnloadAvatarImages

```csharp
public static void UnloadAvatarImages()
```

Unloads all user avatar images from local memory

### UnloadAvatarImage

```csharp
public static void UnloadAvatarImage(Texture2D image)
```

Unloads a specific avatar image from memory

### GetPlayerNickname

```csharp
public static string GetPlayerNickname(UserData userId)
```

This is handled automatically via [UserData](../data-layer/user-data.md).Name. It simply returns the nickname set for this user by the local user if any.

### HasFriend

```csharp
public static bool HasFriend(UserData userId, EFriendFlags flags)
```

Checks if the user meets the specified criteria. (Friends, blocked, users on the same server, etc)

### InviteUserToGame

```csharp
public static bool InviteUserToGame(UserData userId, string connectString)
```

Invites a friend or clan member to the current game using a special invite string.

### IsFollowing

```csharp
public static void IsFollowing(UserData userId, 
                Action<FriendsIsFollowing_t, bool> callback)
```

Checks if the current user is following the specified user.

### IsUserInSource

```csharp
public static bool IsUserInSource(UserData userId, CSteamID sourceId)
```

Checks if a specified user is in a source (Steam group, chat room, lobby, or game server).

### ReplyToFriendMessage

```csharp
public static bool ReplyToFriendMessage(UserData userId, string message)
```

Sends a message to a Steam friend.

### RequestFriendRichPresence

```csharp
public static void RequestFriendRichPresence(UserData userId)
```

Requests Rich Presence data from a specific user.

This is used to get the Rich Presence information from a user that is not a friend of the current user, like someone in the same lobby or game server.

This function is rate limited, if you call this too frequently for a particular user then it will just immediately post a callback without requesting new data from the server.

### RequestUserInformation

```csharp
public static bool RequestUserInformation(UserData userId, bool nameOnly)
```

Requests the persona name and optionally the avatar of a specified user.

### SetInGameVoiceSpeaking

```csharp
public static void SetInGameVoiceSpeaking(bool speaking)
```

Let Steam know that the user is currently using voice chat in game.

### SetListenForFriendsMessages

```csharp
public static void SetListenForFriendsMessages(bool enabled)
```

Listens for Steam friends chat messages.

{% hint style="info" %}
This is done for you when you set the [ListenForFriendsMessages](friends.md#listenforfriendsmessages) field.
{% endhint %}

### SetPersonaName

```csharp
public static void SetPersonaName(string name, 
                Action<SetPersonaNameResponse_t, bool> callback)
```

Sets the current user's persona name, stores it on the server and publishes the changes to all friends who are online.

### SetPlayedWith

```csharp
public static void SetPlayedWith(UserData userId)
```

Mark a target user as 'played with'.

### SetRichPresence

```csharp
public static bool SetRichPresence(string key, string value)
```

Sets a Rich Presence key/value for the current user that is automatically shared to all friends playing the same game.

### GetLoadedAvatar

```csharp
public static Texture2D GetLoadedAvatar(UserData id)
```

Used internally to fetch a preloaded avatar for the indicated user. You shouldn't ever need to call this manually.

### PersonaChangeHasFlag

```csharp
public static bool PersonaChangeHasFlag(EPersonaChange value, 
                                EPersonaChange checkflag)
```

Checks if the value has the indicated flag set&#x20;

### PersonaChangeHasAllFlags

```csharp
public static bool PersonaChangeHasAllFlags(EPersonaChange value, 
                                params EPersonaChange[] checkflags)
```

Checks if the value has all of the flags indicated set

## How To

### Manage Rich Presence

Rich Presence is a powerful social system for full details please read the feature documentation linked below

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

It is often forgot that Steam is a social network. There are multiple groupings of a user's friends that can be read and listed for various uses.

For general use the GetFriends method will return a simple array of UserData representing each friend by its type. This method takes a "flag" representing the type of friend list to return. The options of flags are as follows.

{% hint style="info" %}
The flag parameter is of type [EFriendFlags](https://partner.steamgames.com/doc/api/ISteamFriends#EFriendFlags) defined in the Steamworks namespace.
{% endhint %}

* None\
  `EFriendFlags.k_EFriendFlagNone`\
  No flag.
*   Blocked\
    `EFriendFlags.k_EFriendFlagBlocked`

    The list of blocked users
*   Friendship Requested\
    `EFriendFlags.k_EFriendFlagFriendshipRequested`

    User that have sent a friend invite to the current user
*   Immediate\
    `EFriendFlags.k_EFriendFlagImmediate`

    The current user's "regular" friends
*   Clan Member\
    `EFriendFlags.k_EFriendFlagClanMember`

    Users that are in one of the same (small) steam groups/clans as the user
*   On Game Server\
    `EFrienndFlags.k_EFriendFlagOnGameServer`

    Users that are on the same game server (as set by SetPlayedWith)
*   Requesting Freindship\
    `EFriendFlags.k_EFriendFlagRequestingFriendship`

    Users that the current user has sent a friend invite to
*   Requesting Info\
    `EFriendFlags.k_EFriendFlagRequestingInfo`

    Users that are currently sending additional info about themselves after a call to RequestUserInformation
*   Ignored\
    `EFriendFlags.k_EFriendFlagIgnored`

    Users that the current user has ignored from contacting them
*   Ignored Friend\
    `EFriendFlags.k_EFriendFlagIgnoredFriend`

    Users that have ignored the current user; but the current still knows about them
*   Chat Member\
    `EFriendFlags.k_EFriendFlagChatMember`

    Users in one of the same chats
*   All\
    `EFriendFlags.k_EFriendFlagAll`

    Returns all friend flags

```csharp
var friends = API.Friends.Client.GetFriends(flag);
```

For example if you wanted to get the "normal" list of friends as seen in the client friend list you might do.

```csharp
var friends = API.Friends.Client.GetFriends(EFriendsFlag.k_EFriendFlagImmediate);
foreach(UserData user in friends)
{
    Debug.Log(user.Name + " is my friend.");
}
```



Alternatively friends can be read from a given source. Sources can include groups/clans, chat rooms, lobbies or game servers.

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

In most cases all of the information you need about a user (or friend) is provided in the UserData returned by these calls. In some cases you may need specific data not accessible through UserData.

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

Finally you can invite friends to join a specific lobby through the Lobby object its self. This assumes you have your Lobby as provided by the API.Matchmaking system.

```
lobby.InviteUserToLobby(user);
```

### Chatting

Its possible to handle friend chat in game via the Friends API. To get started you must enable the listen for friends messages

```
API.Friends.Client.ListenForFriendsMessages = true;
```

Setting this value to value will disable the system, this can be enabled and disabled at will.

Once enabled the API.Friends.Client.EventGameConnectedFriendChatMsg event will be raised any time a new message is received. The event will contain information about the message which can be used to present the message to a Chat UI.

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

To send a response to a given player e.g. to send a chat message your self use

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
UserData objects can be used to fetch persona state, name and other information typically in a simpler method than using the Friends interface directly.
{% endhint %}

```csharp
var state = API.Friends.Client.PersonaState;
```

and to get the persona state for any other user you can use

```csharp
var state = API.Friends.Client.GetFriendPersonaState(user);
```

### Requesting User Information

In most cases this is not necessary, Steam will generally already have the information for users that the local user "knows" including:

* Friends
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
