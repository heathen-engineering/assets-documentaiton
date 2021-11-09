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

### Fields and Attributes

| Type              | Name     | Comments                                                                             |
| ----------------- | -------- | ------------------------------------------------------------------------------------ |
| CSteamID          | cSteamId | The raw CSteamID of this user                                                        |
| Texture2D         | Avatar   | Gets the user's avatar if its available. If this is null you should call LoadAvatar. |
| string            | Name     | The display name of the user as seen in Steam friends.                               |
| EPersonaState     | State    | The current persona state of the user.                                               |
| bool              | InGame   | Is the user in game                                                                  |
| FriendGameInfo\_t | GameInfo | returns information about the game the user is in if any.                            |
| int               | Level    | returns the user's current Steam level.                                              |

### Methods

```csharp
public void LoadAvatar(Action<Texture2D> callback);
```

Functionally the same as calling `API.Friends.Client.GetFriendAvatar(user.cSteamId)` . This starts the process of loading the avatar image from Steam cashe if its not already loaded into memory.

The callback on this method will include the loaded texture, the loaded texture can also be found via user.Avatar.

```csharp
public bool GetGamePlayed(out FriendGameInfo_t gameInfo);
```

Functionally the same as calling `API.Friends.Client.GetFriendGamePlayed(user.cSteamId, out results)`. This returns rather or not the user is in a game and if so the results will be populated with information about that game.

```csharp
public static UserData Get( .. );
```

This method is a static method that can be used to fetch the user data for any given user or for the local user. You can pass in a CSteamID or its ulong equivlent to fetch the user data for other users. If you do not pass in an id this method will return the local user's user data.
