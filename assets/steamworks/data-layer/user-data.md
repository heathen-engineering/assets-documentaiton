---
description: Useing Steam User Data
---

# User Data

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

The UserData object provides quick and efficent access to the details and artifacts pertaining to any given user. Heathen's UserData object is interchaingable with CSteamID and ulong and can be created by simply casting or assigning from those values.

```csharp
UserData user_fromUlong = 1234566;
UserData user_fromCSteamID = new CSteamID(1234566);
UserData user = UserData.Get(1234566);

//A static helper to geet the local user's UserData object
UserData thisUser = UserData.Me;
```

The UserData object is a structure and as such is a value type, it only stores the CSteamID of the user it relates to and reads all other information at the time of request from Steam's local cashe. As this object reads from Steam cashe it is possible to try to read data for a user that is not cashed resulting in empty or partial information.

In general you can only access user information for a user that the local user "knows". This is defined by Steam as users that:

* Are friends
* Share a clan or group (some limitations apply regarding large groups)
* Share a lobby
* Share a game server

You may be able to get limited information for additional users such as user's found on a leaderboard that you have quried.

If you need to request information for a user your local user does not "know" you should call `API.Friends.Client.RequestUserInformation(user, getNameOnly)`. You should avoid doing this if possible, in most cases there is no reason to get a user's information for a user that the local user does not "know".

## Fields and Attributes

### Me

```csharp
public static UserData Me => get;
```

This simply returns the local user's UserData and is the same as calling `API.User.Client.Id`

### ID

```csharp
public CSteamID id;
```

The underlying native ID for this clan

### SteamId

```csharp
public ulong SteamId { get; set; }
```

The underlying ulong value of the CSteamID&#x20;

### AccountId

```csharp
public AccountID_t { get; set; }
```

The account ID segment of the full CSteamID, to understand more read [this article](../unity/quick-start-guide/csteamid.md).

### FriendId

```csharp
public uint FriendId { get; set; }
```

The underlying uint value of the AccountID\_t segment of the CSteamID, to understand more read [this article](../unity/quick-start-guide/csteamid.md).

### IsValid

```csharp
public bool IsValid => get;
```

This indicates rather or not the underlying CSteamID is of the proper Universe and Type it does not indicate that it is a valid entry. E.g. this tells you if the data is of the right shape ... not that it equates to a valid entry in Steam client.

### IsMe

```csharp
public bool IsMe => get;
```

This is true if this UserData object is the local user

### Avatar

{% hint style="info" %}
You can use the [SetUserAvatar](../unity/components/set-user-avatar.md) component to more easily manage a given user's avatar texture. The [SetUserAvatar](../unity/components/set-user-avatar.md) componenet will assign a RawImage with the texture and will monitor Steam API for changes to that avatar thus if that user changes there avatar image it will automatically update the RawImage texture.
{% endhint %}

```csharp
public Texture2D Avatar => get;
```

This is the texture loaded for this user's avatar if it has been loaded. Note you must call LoadAvatar for this user before this value will be set i.e.

```csharp
if(user.Avatar == null)
    user.LoadAvatar((result) =>
    {
        rawImage.texture = result;
    });
else
    rawImage.texture = user.Avatar;
```

### Name

{% hint style="info" %}
You can use the [SetUserName](../unity/components/set-user-name.md) component to more easily manage a given user's name. The [SetUserName ](../unity/components/set-user-name.md)componenet will assign a uGUI Text or TMPro Text with the name or nickname of the indicated user and will update it if that name should change.
{% endhint %}

```csharp
public string Name => get;
```

This reads the user's Steam Name

### Nickname

{% hint style="info" %}
You can use the [SetUserName](../unity/components/set-user-name.md) component to more easily manage a given user's name. The [SetUserName ](../unity/components/set-user-name.md)componenet will assign a uGUI Text or TMPro Text with the name or nickname of the indicated user and will update it if that name should change.
{% endhint %}

```csharp
public string Nickname => get;
```

This reads the nickname set for this user by the local user if any. If none then this will be the same as Name.

### State

```csharp
public EPersonaState State => get;
```

Returns the [EPersonaState](https://partner.steamgames.com/doc/api/ISteamFriends#EPersonaState) value for this user.

### InGame

```csharp
public bool InGame => get;
```

Is this user in a game?

### GameInfo

```csharp
public FriendGameInfo_t GameInfo => get;
```

Returns the [FriendGameInfo\_t](https://partner.steamgames.com/doc/api/ISteamFriends#FriendGameInfo\_t) discribing the game ID, connection information and lobby ID if any that this user is related to.

### Level

```csharp
public int Level => get;
```

Gets the Steam user level for this user.

### AccountId

```csharp
public AccountID_t AccountId => get;
```

Returns the [AccountID\_t](https://partner.steamgames.com/doc/api/steam\_api#AccountID\_t) also called a "Friend ID" this is mostly used internally by Steam API but is used in a few API calls such as UGC Query.

### FriendId

```csharp
public uint FriendId => get;
```

Returns the uint value of the AccountId.

## Methods

### ClearRichPresence

```csharp
public static void ClearRichPresence()
```

Clears the rich presence data for the local user.

### Get

```csharp
public static UserData Get( .. );
```

This method is a static method that can be used to fetch the user data for any given user or for the local user. You can pass in a CSteamID or its ulong equivlent to fetch the user data for other users. If you do not pass in an id this method will return the local user's user data.

### GetGamePlayed

```csharp
public bool GetGamePlayed(out FriendGameInfo_t gameInfo);
```

Functionally the same as calling `API.Friends.Client.GetFriendGamePlayed(user.cSteamId, out results)`. This returns rather or not the user is in a game and if so the results will be populated with information about that game.

### InviteToGame

```csharp
public void InviteToGame(string connectString)
```

Invites the target user to a game passing in the connection string. This will cause the [GameRichPrecenseJoinRequest](../api/overlay.md#game-rich-presence-join-requested) event to be raised on the invited user if present in game, or will launch the game with the connectionString in the command line if not.

### InviteToLobby

```csharp
public bool InviteToLobby(Lobby lobby)
```

Invites the target user to join a specific lobby. This will cause the [GameLobbyJoinRequest ](../api/overlay.md#game-lobby-join-requested)event to be raised on the invited user when accepted if present in game or will launch the game with the lobby ID in the command line if not in game.

### LoadAvatar

```csharp
public void LoadAvatar(Action<Texture2D> callback);
```

Functionally the same as calling `API.Friends.Client.GetFriendAvatar(user.cSteamId)` . This starts the process of loading the avatar image from Steam cashe if its not already loaded into memory.

The callback on this method will include the loaded texture, the loaded texture can also be found via user.Avatar.

```csharp
//Assuming a RawImage named rawImage;
user.LoadAvatar((result) =>
{
    rawImage.texture = result;
});
```

### SendMessage

```csharp
public bool SendMessage(string message);
```

Sends the user a message via the Replay To Friend feature.

If this returns false then the current user is rate or chat limited by Valve.

### SetRichPresence

```csharp
public static bool SetRichPresence(string key, string value)
```

Sets a rich presence value on the local user.
