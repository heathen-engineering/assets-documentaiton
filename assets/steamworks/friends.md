---
description: List your user friends, open chats, send invites and much more!
---

# Friends

## Introduction

In Heathen's integration, we use the term "Friends" as a concept and not a specific tool. Valve uses "Friends" as a specific interface/tool in the Steam API, so this term may be slightly confusing for users of the raw Steam API. For example the Clans tool from Heathen Engineering uses parts of Valve's Steam Friends interface as does the UserData object and Leaderboard object.

For the context of Heathen, the "Friends" tools are tools in the SteamSettings.Client that deal with browsing, chatting to or managing a user's friends and is not limited to or inclusive of all features of "Steam Friends" interface as defined by Valve.&#x20;

### Clans and Groups

For information on the Clans aka Steam Groups feature, please see the following article

{% embed url="https://kb.heathenengineering.com/assets/steamworks/clans" %}

## Examples

### Get UserData

You can fetch details about a friend via Heathen's `UserData` object. This object contains common information such as display name, avatar, etc. and provides access to user specific features such as sending messages and getting rich presence information.

{% hint style="info" %}
Note in most cases you don't need to call this manually, as our system will have already fetched the UserData objects for a given list. Such as members of a lobby, members on a server or the members of your friend list such as via `SteamSettings.Client.ListFriends();` &#x20;

Also don't worry about calling this multiple times. We cash results as does Valve so calling it multiple times on a single user will not incur any network traffic, as the data is only fetched and updated when need be.
{% endhint %}

```csharp
var myFriend = SteamSettings.Client.GetUserData(friendId);
```

### List the user's friends

```csharp
public List<UserData> SteamSettings.Client.ListFriends(EFriendFlags flags);
```

flags defaults to `k_EFriendFlagImmediate` which is the "normal" friends that you would see listed in say your Steam Friends list in the Steam Overlay. For a complete list of each flag and what it does please read the following documentation

{% embed url="https://partner.steamgames.com/doc/api/ISteamFriends#EFriendFlags" %}

### Get follower count

To list the number of users following a specific user.

```csharp
public void SteamSettings.Client.GetFollowerCount
    (CSteamID followingThisUser, 
    Action<UserData user, int count>);
```

For this method, you pass in the user you want to get the count for and an action you want invoked when the operation is complete. That action will have the user you passed in and the number of users following them.&#x20;

For example

```csharp
SteamSettings.Client.GetFollowerCount(SteamSettings.Client.user,
    (user, count) =>
    {
        Debug.Log("The local user with ID: " + user +
        " has " + count + " users following it.");
    });
```

### Set rich presence information

You may have noticed in Steam Friends list that extra data about the game your friend is playing can be displayed. There are several special use cases for this but all use the following syntax to set the values.

```csharp
public bool SteamSettings.Client.SetRichPresence(string key, string value);
```

Please consult Valve's documentation for details on the unique use cases

{% embed url="https://partner.steamgames.com/doc/api/ISteamFriends#SetRichPresence" %}

#### Set "Status"

This is a string that shows in the "View Game Info" dialog in the Steam Friends list.

```csharp
SteamSettings.Client.SetRichPresence("status", "Shows in view game info dialog");
```

#### Set "Connect"

This is a string that contains the command-line for how a friend can connect to a game. This enables the "Join Game" button in the "View Game Info" dialog, in the steam friends list right click menu and on the player's Steam community profile.

{% hint style="info" %}
Be sure your app implements

[SteamApps.GetLaunchCommandLine](https://partner.steamgames.com/doc/api/ISteamApps#GetLaunchCommandLine) so you can disable the popup warning when launched via a command line.
{% endhint %}

```csharp
SteamSettings.Client.SetRichPresence("connect", "command line value");
```

#### Set localization token

This sets the localization token that will be displayed in the viewing user's selected language in Steam client UI. See the value documentation on the use of these tokens here.

{% embed url="https://partner.steamgames.com/doc/api/ISteamFriends#richpresencelocalization" %}

```csharp
SteamSettings.Client.SetRichPresence("steam_display", "#Status_AtMainMenu");
```

#### Set player group

When set, this indicates to the Steam client that the player is a member of a particular group. Players in the same group may be organized together in various places in the Steam UI. This string could identify a party, a server, or whatever grouping is relevant for your game. The string itself is not displayed to users.

```csharp
SteamSettings.Client.SetRichPresence("steam_player_group", "group id");
```

#### Set group size

When set, indicates the total number of players in the steam\_player\_group. The Steam client may use this number to display additional information about a group when all of the members are not part of a user's friends list. (For example, "Bob, Pete, and 4 more".)

```csharp
SteamSettings.Client.SetRichPresence("steam_player_group_size", "6");
```

### Get rich presence information

You get the rich presence data from the UserData object its self. You can get the UserData object from a number of sources including listing a user's friends, the members of a lobby or the local user's data via `SteamSettings.Client.user`

#### Get a specific value

```csharp
var friends = SteamSettings.Client.ListFriends();

foreach(var friend in friends)
{
    Debug.Log(friend.DisplayName + " group id = " + 
        friend.GetRichPresenceValue("steam_player_group");
}
```

#### List all values

```csharp
var friends = SteamSettings.Client.ListFriends();

foreach(var friend in friends)
{
    //This is a Dictionary<string, string>
    var presenceValues = friend.GetRichPresenceValues();
    
    foreach(var kvp in presenceValues)
    {
        //kvp.Key is the key
        //kvp.Value is the value of that key
    }
}
```

### Using Friend Chat

{% hint style="warning" %}
It is recommended to use Steam Overlay for friend chat. However it is possible to handle the chat messages directly in game
{% endhint %}

#### Open Chat in Overlay

for a given `UserData` object simply call

```csharp
user.OpenChat();
```

#### To handle chat in game

While its strongly recommended that you use the Steam Overlay to handle friend chat, it is possible to handle chat in your game directly. To do so you first need to enable the feature.

```csharp
SteamSettings.Client.ListenFroFriendMessages(true);
```

You can disable this feature at any time

```csharp
SteamSettings.Client.ListenFroFriendMessages(false);
```

#### Receive messages in game

When enabled the `evtRecievedFriendChatMessage` will be raised with each received message, so you should be listening on this event as such

```csharp
private void HandleFriendChat(UserData friend, string message, EChatEntryType type)
{
    //DO WORK
}
```

and register that handler to the event via

```csharp
SteamSettings.Client.evtRecievedFriendChatMessage.AddListener(HandleFriendChat);
```

#### Send message in game

You can send a friend a message via that friend's UserData object

```csharp
var friends = SteamSettings.Client.ListFriends();

foreach(var friend in friends)
{
    friend.SendMessage("I'm spaming everyone!\nHow rude!!!");
}
```

You can also use the global methods to send to a specific friend by ID such as

```csharp
SteamSettings.Client.SendFriendChatMessage(friendId, message);
```

### Invite to lobby

For this you need to have a reference to the `Lobby` you want to invite the friend to, and you need to know the id of the friend you want invite which you can get from the friend's `UserData`

```csharp
MatchmakingTools.groupLobby.InviteUserToLobby(user.id);
```

For more details on Matchmaking tools including how to handle an invite request, please see the Matchmaking documentation

{% embed url="https://kb.heathenengineering.com/assets/steamworks/multiplayer/matchmaking-tools" %}

### Open friend profile

Assuming you have the `UserData` object of the user.

```csharp
user.OpenProfile();
```

### Open trade

Assuming you have the `UserData` object of the user.

```csharp
user.OpenTrade();
```

### Open stats

Assuming you have the `UserData` object of the user.

```csharp
user.OpenStats();
```

### Open Achievements

Assuming you have the `UserData` object of the user.

```csharp
user.OpenAchievements();
```

### Open Friend Add

Assuming you have the `UserData` object of the user.

```csharp
user.OpenFriendAdd();
```

### Open Friend Remove

Assuming you have the `UserData` object of the user.

```csharp
user.OpenFriendRemove();
```

### Open Friend Request Accept

Assuming you have the `UserData` object of the user.

```csharp
user.OpenRequestAccept();
```

### Open Friend Request Ignore

Assuming you have the `UserData` object of the user.

```csharp
user.OpenRequestIgnore();
```
