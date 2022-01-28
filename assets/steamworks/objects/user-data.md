---
description: Useing Steam User Data
---

# User Data

## Introduction

The UserData object provides quick and efficent access to the details and artifacts pertaining to any given user. Heathen's UserData object is interchaingable with CSteamID and ulong and can be created by simply casting or assigning from those values.

```csharp
UserData user_fromUlong = 1234566;
UserData user_fromCSteamID = new CSteamID(1234566);
UserData user = UserData.Get(1234566);
```

The UserData object is a structure and as such is a value type, it only stores the CSteamID of the user it relates to and reads all other information at the time of request from Steam's local cashe. As this object reads from Steam cashe it is possible to try to read data for a user that is not cashed resulting in empty or partial information.

In general you can only access user information for a user that the local user "knows". This is defined by Steam as users that:

* Are friends
* Share a clan or group (some limitations apply regarding large groups)
* Share a lobby
* Share a game server

You may be able to get limited information for additional users such as user's found on a leaderboard that you have quried.

If you need to request information for a user your local user does not "know" you should call `API.Friends.Client.RequestUserInformation(user, getNameOnly)`. You should avoid doing this if possible, in most cases there is no reason to get a user's information for a user that the local user does not "know".

## Definition

```csharp
public struct UserData;
```

## Fields and Attributes

### cSteamId

```csharp
public CSteamID cSteamId;
```

This is simply the native CSteamID value as used by Steam's APIs you do not need to read or set this directly as the UserData object is implicitly assignable and convertable to CSteamID and ulong.

### IsMe

```csharp
public bool IsMe => get;
```

This is true if this UserData object is the local user

### SteamId

```csharp
public ulong SteamId { get; set; }
```

This gets or sets the ID by its ulong value

### Avatar

{% hint style="info" %}
You can use the [SetUserAvatar](../components/set-user-avatar.md) component to more easily manage a given user's avatar texture. The [SetUserAvatar](../components/set-user-avatar.md) componenet will assign a RawImage with the texture and will monitor Steam API for changes to that avatar thus if that user changes there avatar image it will automatically update the RawImage texture.
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

```csharp
public string Name => get;
```

This reads the user's Steam Name

### Nickname

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

### GetGamePlayed

```csharp
public bool GetGamePlayed(out FriendGameInfo_t gameInfo);
```

Functionally the same as calling `API.Friends.Client.GetFriendGamePlayed(user.cSteamId, out results)`. This returns rather or not the user is in a game and if so the results will be populated with information about that game.

### Get

```csharp
public static UserData Get( .. );
```

This method is a static method that can be used to fetch the user data for any given user or for the local user. You can pass in a CSteamID or its ulong equivlent to fetch the user data for other users. If you do not pass in an id this method will return the local user's user data.
