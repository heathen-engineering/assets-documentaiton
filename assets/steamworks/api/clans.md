---
description: Access the Steam Clan aka Steam Group system with Heathen's Steam API
---

# Clans.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

```csharp
using ClansClient = HeathenEngineering.SteamworksIntegration.API.Clans.Client;
```

```csharp
public static class Clans.Client
```

This leverages features of ISteamFriends, ISteamUser and ISteamUGC to simplify working with Steam "clans" aka "groups" aka "guilds" ... known by a lot of names but these are the "communities" you see in Steam which can have chats, news, etc.

### What is a clan?

Also known as a Community Group, Steam lets user's create there own social groups, these could be groups of active players similar to a guild in an MMO or simply an interest group e.g. a collection of Steam users with similar interests. You can search the existing community groups here:

{% embed url="https://steamcommunity.com/search/groups" %}
Search For Community Groups
{% endembed %}

### What can it do?

You can list the clan owner, its officers, open the clan chat in overlay or join the clan's chat in game. The most common use game developers look for and the most complex is to join the clan chat in game.

### Related Components

{% embed url="https://kb.heathen.group/assets/steamworks/for-unity-game-engine/components/clan-chat-director" %}

### Related Objects

{% embed url="https://kb.heathen.group/assets/steamworks/data-layer/clan-data" %}

{% embed url="https://kb.heathen.group/assets/steamworks/objects/clan-chat-msg" %}

## Events

### EventChatMessageRecieved

```csharp
public static GameConnectedClanChatMsgEvent EventChatMessageRecieved
```

Called when a chat message has been received in a Steam group chat that we are in.

{% hint style="info" %}
Its generally easier to use the [Clan Chat Director](../unity/components/clan-chat-director.md) than to manually listen on this event.
{% endhint %}

The handler for this event should look like this

```csharp
public void HandleEvent(ClanChatMsg arg)
{
    //Do Work
}
```

You can learn more about [ClanChatMsg](../objects/clan-chat-msg.md) in its article.

### EventGameConnectedChatJoin

```csharp
public static GameConnectedChatJoinEvent EventGameConnectedChatJoin
```

Called when a user has joined a Steam group chat that the we are in.

The handler for this event should look like this

```csharp
public void HandleEvent(ChatRoom room, CSteamID user)
{
    //Do Work
}
```

### EventGameConnectedChatLeave

```csharp
public static GameConnectedChatLeaveEvent EventGameConnectedChatLeave
```

Called when a user leaves a Steam group that we are in

The handler for this event should look like this

```csharp
public void HandleEvent(UserLeaveData arg)
{
    //Do Work
}
```



## Fields and Attributes

### JoinedChatRooms

```csharp
public static ChatRoom[] JoinedChatRooms = get;
```

This is provided for debugging purposes and generally shouldn't be used

## Methods

### JoinChatRoom

```csharp
public static void JoinChatRoom(CSteamID clanId, 
                Action<ChatRoom, bool> callback)
```

Joins the chat for a target clan

The callback for this method should look like this

```csharp
public void HandleCallback(ChatRoom room, bool IOError)
{
    //Do Work
}
```

### LeaveChatRoom

```csharp
public static void LeaveChatRoom(CSteamID clanChatId)
```

```csharp
public static void LeaveChatRoom(ChatRoom clanChat)
```

Leaves a specific chat room

### GetChatMemberByIndex

```csharp
public static CSteamID GetChatMemberByIndex(CSteamID clan, int index)
```

Gets the Steam ID at the given index in a Steam group chat.

### GetActivityCounts

```csharp
public static bool GetActivityCounts(CSteamID clan, 
                        out int online, 
                        out int inGame, 
                        out int chatting)
```

Gets the most recent information we have about what the users in a Steam Group are doing.

* clan\
  The group to get the activity for
* online\
  The number of members that are online
* inGame\
  The number of members that are in game
* chatting\
  The number of members that are in the chat group

### GetClanByIndex

```csharp
public static Clan GetClanByIndex(int clanIndex)
```

Gets the Steam group's Steam ID at the given index. Get the number of clans using the GetClanCount method.

{% hint style="info" %}
Its generally simpler to just call GetClans() and return the whole array at once
{% endhint %}

### GetClans

```csharp
public static Clan[] GetClans()
```

Get the list of clans the current user is a member of

### GetChatMemberCount

```csharp
public static int GetChatMemberCount(CSteamID clanId)
```

Get the number of users in a Steam group chat.

### GetChatMembers

```csharp
public static UserData[] GetChatMembers(CSteamID clanId)
```

Returns a list of the members of the given clans chat

Get the number of users in a Steam group chat. This is used for iteration, after calling this then GetChatMemberByIndex can be used to get the Steam ID of each person in the chat.

{% hint style="warning" %}
Large steam groups cannot be iterated by the local user.
{% endhint %}

### GetChatMessage

```csharp
public static string GetChatMessage(ChatRoom clanChat, 
                                        int index, 
                                        out EChatEntryType type, 
                                        out CSteamID chatter)
```

You generally do not need to call this if your using the [EventChatMessageReceievd ](clans.md#eventchatmessagerecieved)or the [ClanChatDirector](../unity/components/clan-chat-director.md).

This gets the data regarding a specific chat message in given clan chat room.

* clanChat\
  The ID of the group chat room to read
* index\
  The index of the message, this should be the m\_iMessageID fireld of the callback if your using the raw API
* type\
  The type of chat entry that was received
* chatter\
  The ID of the user that caused the message

### GetClanCount

```csharp
public static int GetClanCount()
```

Gets the number of Steam groups that the current user is a member of.

### GetName

```csharp
public static string GetName(Clan clanId)
```

Gets the display name for the specified Steam group; if the local client knows about it.

### GetOfficerByIndex

```csharp
public static UserData GetOfficerByIndex(Clan clanId, int officerIndex)
```

Gets the Steam ID of the officer at the given index in a Steam group.

### GetOfficers

```csharp
public static UserData[] GetOfficers(Clan clanId)
```

Gets the list of officers for the given clan.

### GetOfficersCount

```csharp
public static int GetOfficerCount(Clan clanId)
```

Gets the number of officers (administrators and moderators) in a specified Steam group. This also includes the owner of the Steam group. This is used for iteration, after calling this then GetClanOfficerByIndex can be used to get the Steam ID of each officer.

### GetOwner

```csharp
public static CSteamID GetOwner(Clan clanId)
```

Gets the owner of a Steam Group.

### GetTag

```csharp
public static string GetTag(Clan clanId)
```

Gets the unique tag (abbreviation) for the specified Steam group; If the local client knows about it. The Steam group abbreviation is a unique way for people to identify the group and is limited to 12 characters.In some games this will appear next to the name of group members.

### OpenChatWindowInSteam

```csharp
public static bool OpenChatWindowInSteam(CSteamID clanChatRoomId)
```

```csharp
public static bool OpenChatWindowInSteam(ChatRoom clanChat)
```

Opens the specified Steam group chat room in the Steam UI.

### SendChatMessage

```csharp
public static bool SendChatMessage(CSteamID clanChatId, string message)
```

```csharp
public static bool SendChatMessage(ChatRoom clanChat, string message)
```

Sends a message to a Steam group chat room.

### IsClanChatAdmin

```csharp
public static bool IsClanChatAdmin(CSteamID clanChatId, CSteamID userId)
```

```csharp
public static bool IsClanChatAdmin(ChatRoom clanChat, CSteamID userId)
```

Is the indicated user a admin for this clan chat

### IsClanPublic

```csharp
public static bool IsClanPublic(Clan clanId)
```

### IsClanOfficialGameGroup

```csharp
public static bool IsClanOfficialGameGroup(CSteamID clanId)
```

Checks if the Steam group is an official game group/community hub.

### IsClanChatWindowOpenInSteam

```csharp
public static bool IsClanChatWindowOpenInSteam(CSteamID clanChatId)
```

Checks if the Steam Group chat room is open in the Steam UI.

### RequestClanOfficerList

```csharp
public static void RequestClanOfficerList(CSteamID clanId, 
                Action<ClanOfficerListResponse_t, bool> callback)
```

### CloseClanChatWindowInSteam

```csharp
public static bool CloseClanChatWindowInSteam(CSteamID clanChatId)
```

```csharp
public static bool CloseClanChatWindowInSteam(ChatRoom clanChat)
```

Closes the specified Steam group chat room in the Steam UI.

### DownloadClanActivityCounts

```csharp
public static void DownloadClanActivityCounts(CSteamID[] clans, 
                Action<DownloadClanActivityCountsResult_t, bool> callback)
```

Refresh the Steam Group activity data or get the data from groups other than one that the current user is a member.

## How To

### Create a Clan / Group

This cannot be done from within the Steam API at current you can however direct your player's to the appropriate location in Steam to create there own clans.

> [https://steamcommunity.com/actions/GroupCreate](https://steamcommunity.com/actions/GroupCreate)

The above URL can be passed into the Steam Overlay

```csharp
API.Overlay.Client.ActivateGameOverlayToWebPage
    ("https://steamcommunity.com/actions/GroupCreate");
```

### Get Clans / Groups

Return an array of the clans the user is a member of

```csharp
Clan[] clans = API.Clans.Client.GetClans();
```

The Clan object contains various helpful members such as Clan.Name, ClanOwner, Clan.JoinChat and more.

### List Clan officers

Using the Clan object

```csharp
UserData[] officers = clan.Officers
```

