# Lobby

## Introduction

The Lobby object is a custom CSteamId that carries tools and funcitons unique to the Steam Lobby system.

{% hint style="info" %}
You can convert a Lobby to a ulong or CSteamID or convert a ulong or CSteamID to a Lobby implicitly e.g.



```csharp
Lobby myLobby = new CSteamID(ulongId);
```

or

```csharp
ulong id = myLobby;
```

or

```csharp
CSteamID id = myLobby;
```
{% endhint %}

All data is read on demand and is always up todate with the Lobby object. The only information it stores in local memory is the ID of the lobby its operating on.

### Constants

The following are constant strings used internally to manage Heathen standard metadata values

*   DataName

    key = name
*   DataVersion

    key = z\_heathenGameVersion
*   DataReady

    key = z\_heathenReady
*   DataKick

    key = z\_heathenKick
* DataMode
* key = z\_heathenMode
* DataType
* key = z\_heathenType

## Definition

```csharp
public struct Lobby : IEquatable<CSteamID>, IEquatable<ulong>
```

## Fields and Attributes

| Type            | Name               | Notes                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| CSteamID        | id                 | The native id of the lobby                                                                                                                                                                                                                                                                                                                                                                                             |
| string          | Name               | <p>the name of the lobby if stored in the lobbies metdata else this returns blank.</p><p></p><p>This can be used by the owner of the lobby to set the lobby name</p>                                                                                                                                                                                                                                                   |
| LobbyMember     | Owner              | <p>Returns the lobby owner's LobbyMember object</p><p></p><p>This can be used by the owner to set a new user as owner</p>                                                                                                                                                                                                                                                                                              |
| LobbyMember     | User               | Gets the local user's LobbyMember entry                                                                                                                                                                                                                                                                                                                                                                                |
| LobbyMember\[]  | Members            | Gets an array of all the members in this lobby                                                                                                                                                                                                                                                                                                                                                                         |
| bool            | IsTypeSet          | Does the system know what type of lobby this is e.g. public, private, friend, etc.                                                                                                                                                                                                                                                                                                                                     |
| ELobbyType      | Type               | <p>If IsTypeSet is true this will return the type of lobby this is set as.</p><p></p><p>Else this will return Private as a default but is not accurate.</p><p></p><p>Note Steam gives no way to accuratly read lobby type so we depend on the Heathen system setting the Type value.</p><p></p><p>The owner of the lobby can use this to set a new type value changing the lobby type and updating the Type field.</p> |
| string          | GameVersion        | Gets or sets (owner only) the game version this lobby's owner is running on                                                                                                                                                                                                                                                                                                                                            |
| bool            | IsOwner            | True if the local user is the owner of the lobby                                                                                                                                                                                                                                                                                                                                                                       |
| bool            | HasServer          | true if the lobby has game server data set                                                                                                                                                                                                                                                                                                                                                                             |
| LobbyGameServer | GameServer         | The current set game server data                                                                                                                                                                                                                                                                                                                                                                                       |
| bool            | AllPlayersReady    | true if all players have indicated they are ready to play                                                                                                                                                                                                                                                                                                                                                              |
| bool            | AllPlayersNotReady | true if all players have indicated they are not ready to play e.g. all are false                                                                                                                                                                                                                                                                                                                                       |
| bool            | IsReady            | read and sets the local user's IsReady status                                                                                                                                                                                                                                                                                                                                                                          |
| bool            | Full               | Is the lobby full e.g. max slots used                                                                                                                                                                                                                                                                                                                                                                                  |
| int             | MaxMembers         | gets the max member count and can be used by the owner to change the max member count                                                                                                                                                                                                                                                                                                                                  |
| string          | \[string key]      | <p>indexer you can use this to access metadata e.g. set or read metadata.</p><p>Only the owner can set metadata</p>                                                                                                                                                                                                                                                                                                    |

## Methods

### this\[string key]

```csharp
public string this[string key]

// Example
lobby["name"] = "New name";
// and
var name = lobby["name"];
```

read and write metadata values on the lobby much as you would access members in a dictionary.

This will never throw a key not found exception, if a key is not present it will simply return an empty string.

### Set Type

```csharp
public bool SetType(type);
```

Funcitonally the same as setting the Type field, this only works for the owner of the lobby

### Set Joinable

```csharp
public bool SetJoinable(bool makeJoinable);
```

Sets the lobby as joinable or not. A lobby always starts as joinable, a lobby that is not joinable cannot be joined by anyone not even a friend or an invited user. This can only be used by the owner of the lobby.

### Get Metadata

```csharp
Dictionary<string, string> GetMetadata();
```

Returns all the metadata for the lobby as a string dictionary. This creates the dictionary each time it is called so cashe the value before use or read the values directly from the lobby such as via the indexer.

### Leave

```csharp
public void Leave();
```

Leaves the lobby, if the owner leaves Steam will assigne a new owner.

### Delete Lobby Data

```csharp
public bool DeleteLobbyData(string key);
```

Removes the indicated metadata entry if present, can only be used by the owner of the lobby

### Invite User to Lobby

```csharp
public bool InviteUserToLobby(UserData user);
```

Invites the indiated user to the lobby

### Send Chat Message

```csharp
public bool SendChatMessage(string message);
```

```csharp
public bool SendChatMessage(byte[] data);
```

Sends a message over the Lobby chat system. See the [Lobby Chat Director](../components/lobby-chat-director.md) for more information.

### Set Game Server

```csharp
public void SetGameServer(string address, ushort port, CSteamID id);
```

```csharp
public void SetGameServer(string address, ushort port);
```

```csharp
public void SetGameServer(CSteamID id);
```

Sets the Game Server information and causes the EventLobbyGameServer event to be raised on the [Matchmaking ](../api/matchmaking.md)interface and on any attached [Lobby Manager](../components/lobby-manager.md) componenets.

### Kick Member

```csharp
public bool KickMember(CSteamID memberId);
```

Marks the ID as a member that should be removed from the lobby. This simply sets the ID to a "kick list" on the lobbies metadata and will cause the EventLobbyAskedToLeave event to be raised for the effected user on the event is present on the [Matchmaking](../api/matchmaking.md) interface and [Lobby Manager](../components/lobby-manager.md).

### Kick List Contains

```csharp
public bool KickListContains(CSteamID memberID);
```

Does the kick list contain the members ID;

### Remove from Kick List

```csharp
public bool RemoveFromKickList(CSteamID memberID);
```

Removes a member from the kick list if present

### Clear Kick List

```csharp
public bool ClearKickList();
```

Clears the kick list

### Get Kick List

```csharp
public CSteamID[] GetKickList();
```

Gets a list of the IDs in the kick list. This must build the array every time its called so cashe the results and only update when needed.

### Set Member Metadata

```csharp
public void SetMemberMetadata(string key, string value);
```

Set metadata on the local user's LobbyMember

### Get Member Metadata

```csharp
public string GetMemberMetadata(string key);
```

Gets the metadata field from the local user's LobbyMember

```csharp
public string GetMemberMetadata(CSteamID memberId, string key);
```

```csharp
public string GetMemberMetadata(LobbyMember member, string key);
```

Gets the metadata field for the indiacated user
