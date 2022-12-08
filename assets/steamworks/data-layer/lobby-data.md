---
description: Steam Lobby Functionality in an easy to use struct
---

# Lobby Data

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct LobbyData : IEquatable<CSteamID>, 
                          IEquatable<ulong>, 
                          IEquatable<LobbyData>
```

The LobbyData object is a custom CSteamId that carries tools and functions unique to the Steam Lobby system. This object is common between both Unity and Godot game engine integrations.

{% hint style="info" %}
You can convert a Lobby to a ulong or CSteamID or convert a ulong or CSteamID to a Lobby implicitly e.g.



```csharp
LobbyData myLobby = new CSteamID(ulongId);
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

All data is read on demand and is always up to date with the Lobby object. The only information it stores in local memory is the ID of the lobby its operating on.

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

## Fields and Attributes

### All Players Not Ready

```csharp
public bool AllPlayersNotReady => get;
```

{% hint style="warning" %}
This iterates over the Members array
{% endhint %}

Returns true if all of the players 'IsReady' is false

### All Players Ready

```csharp
public bool AllPlayersReady => get;
```

{% hint style="warning" %}
This iterates over the Members array
{% endhint %}

Returns true if all of the players 'IsReady' is true

### AccountId

```csharp
public AccountID_t { get; set; }
```

The account ID segment of the full CSteamID, to understand more read [this article](../unity/quick-start-guide/csteamid.md).

### Friend Id

```csharp
public uint FriendId { get; set; }
```

The underlying uint value of the AccountID\_t segment of the CSteamID, to understand more read [this article](../unity/quick-start-guide/csteamid.md).

### Full

```csharp
public bool Full => get;
```

Returns true if the lobby is full e.g. has no more open slots

### Game Server

```csharp
public LobbyGameServer GameServer => get;
```

Returns the lobby game server data if any

### Game Version

```csharp
public string GameVersion { get; set; }
```

Gets or sets the version of the game the lobby is configured for ... this should match the owners version. This can only be set by the owner of the lobby.

### Has Server

```csharp
public bool HasServer => get;
```

Does this lobby have a game server registered to it

### Is Group

```csharp
public bool IsGroup { get; set; )
```

Indicates rather or not this lobby is a group (aka party) lobby. When set to true a metadata value \`z\_heathenMode\` will be set to \`Group\` and the lobby type will be set to a invisible.

### Is Owner

```csharp
public bool IsOwner => get;
```

Returns true if the local user is the owner of this lobby

### IsReady

```csharp
public bool IsReady { get; set; }
```

Sets the ready flag for this player on this lobby

### IsSession

```csharp
public bool IsSession { get; set; }
```

Indicates rather or not this lobby is a session lobby. When set to true a metadata value \`z\_heathenMode\` will be set to \`Session\`. Lobby type is not automatic set when writing to this field. Session type lobbies can technically be of any type.

### IsTypeSet

```csharp
public bool IsTypeSet => get;
```

This returns true if the Lobby Type is known

### IsValid

```csharp
public bool IsValid => get;
```

This indicates rather or not the underlying CSteamID is of the proper Universe and Type it does not indicate that it is a valid entry. E.g. this tells you if the data is of the right shape ... not that it equates to a valid entry in Steam client.

### Me

```csharp
public LobbyMemberData User => get;
```

Returns the local user's [LobbyMember ](lobby-member-data.md)value for this Lobby.

### Members

```csharp
public LobbyMemberData[] Members => get;
```

{% hint style="warning" %}
this must create the array each time it is called, so call it once, cash it and use it do not call it multiple times a frame.
{% endhint %}

Returns an array of all the lobby members.

### Max Members

```csharp
public int MaxMembers { get; set; } 
```

Gets or sets the max members permitted in this lobby, this can only be set by the owner.

### Member Count

```csharp
public int MemberCount => get;
```

Returns the number of members currently in this lobby

### Name

```csharp
public string Name { get; set; }
```

The name of the lobby if stored in the lobby's metadata. Only the owner of the lobby can set this value.

### Owner

```csharp
public LobbyMemberData Owner { get; set; }
```

The [LobbyMember ](lobby-member-data.md)data for the owner of the lobby, only the current owner can set this value to some other [LobbyMember](lobby-member-data.md).



### SteamId

```csharp
public ulong SteamId { get; set; }
```

The underlying ulong value of the CSteamID&#x20;

### Type

```csharp
public ELobbyType Type { get; set; }
```

Returns the type of the lobby if set, if not set this will default to Private, you can check if the type is set with IsTypeSet. Only the owner of the lobby can set this value.

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

Functionally the same as setting the Type field, this only works for the owner of the lobby

### Set Joinable

```csharp
public bool SetJoinable(bool makeJoinable);
```

Sets the lobby as joinable or not. A lobby always starts as joinable, a lobby that is not joinable cannot be joined by anyone not even a friend or an invited user. This can only be used by the owner of the lobby.

### Get Metadata

```csharp
Dictionary<string, string> GetMetadata();
```

Returns all the metadata for the lobby as a string dictionary. This creates the dictionary each time it is called so cashé the value before use or read the values directly from the lobby such as via the indexer.

### Create

We have a number of static create methods you can use to quickly create common types of lobbies.

```csharp
//Create any type of lobby
public static void Create(ELobbyType type, 
                          int slots, 
                          Action<EResult, LobbyData, bool> callback)
```

```csharp
//Create an invisible lobby and set the type field to "Group"
//This allows the LobbyData.GetGroup(...) to find this lobby
public static void CreateParty(int slots, Action<EResult, LobbyData, bool> callback)
```

```csharp
//Create a lobby of any type and set its type field to "Session"
//This allows the LobbyData.GetSession(...) to find this lobby
public static void CreateSession(ELobbyType type, 
                                 int slots, 
                                 Action<EResult, LobbyData, bool> callback)
```

```csharp
//Create a lobby of type Public and set its type field to "Session"
//This allows the LobbyData.GetSession(...) to find this lobby
public static void CreatePublicSession(int slots, Action<EResult, LobbyData, bool> callback)
```

```csharp
//Create a lobby of type Private and set its type field to "Session"
//This allows the LobbyData.GetSession(...) to find this lobby
public static void CreatePrivateSession(int slots, Action<EResult, LobbyData, bool> callback)
```

```csharp
//Create a lobby of type Friend Onl and set its type field to "Session"
//This allows the LobbyData.GetSession(...) to find this lobby
public static void CreateFriendOnlySession(int slots, Action<EResult, LobbyData, bool> callback)
```

### Join

```csharp
public void Join(Action<LobbyEnter_t, bool> callback);
```

This attempts to join the player to this lobby. The callback parameter of this event expects a handler method such as

```csharp
private void Handler(LobbyEnter_t result, bool IOError)
{
    //Do Work
}
```

This method has several static overloads that can be useful for friend join UI features and similar

```csharp
public static void Join(string accountId, Action<LobbyEnter_t, bool> callback)
```

```csharp
public static void Join(AccountID_t accountId, Action<LobbyEnter_t, bool> callback)
```

```csharp
public static void Join(Lobby lobby, Action<LobbyEnter_t, bool> callback)
```

In all cases these static members fetch the lobby indicated by either an account ID or the Lobby value its self and then attempts to join it. The callback parameter takes the same for as the instanced method.

### Leave

```csharp
public void Leave();
```

Leaves the lobby, if the owner leaves Steam will assigne a new owner.

### Get

```csharp
public static LobbyData Get(uint accountId);
```

```csharp
public static LobbyData Get(AccountId_t accountId);
```

```csharp
public static LobbyData Get(ulong id);
```

```csharp
public static LobbyData Get(CSteamID id);
```

These methods simply return a valid Lobby object representing the lobby indicated by the provided data.

### Group Lobby

```csharp
public static bool GroupLobby(out LobbyData lobby)
```

Get the group lobby the user is a member of if any

```csharp
if(LobbyData.GroupLobby(out var lobby))
{
    //The user is a member of lobby and it is a group lobby
}
else
{
    //The user is not in a lobby labeled as a Group lobby
}
```

### Session Lobby

```csharp
public static bool SessionLobby(out LobbyData lobby)
```

Get the session lobby the user is a member of if any

```csharp
if(LobbyData.SessionLobby(out var lobby)
{
    //The user is a member of lobby and it is a session lobby
}
else
{
    //The user is not in a lobby labeled as a Session lobby
}
```

### Delete Lobby Data

```csharp
public bool DeleteLobbyData(string key);
```

Removes the indicated metadata entry if present, can only be used by the owner of the lobby

### Invite User to Lobby

```csharp
public bool InviteUserToLobby(UserData user);
```

Invites the indicated user to the lobby

### Send Chat Message

```csharp
public bool SendChatMessage(string message);
```

```csharp
public bool SendChatMessage(byte[] data);
```

```csharp
public bool SendChatMessage(object jsonObject);
```

Sends a message over the Lobby chat system. You can use tools like the [Lobby Chat Director](../unity/components/lobby-chat-director.md) to help you manage incoming chat messages.

Note that Steam's lobby chat sends byte\[] data so it can send more than simple text if you need.

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

Sets the Game Server information and causes the EventLobbyGameServer event to be raised on the [Matchmaking ](../api/matchmaking.md)interface and on any attached [Lobby Manager](../unity/components/lobby-manager.md) componenets.

### Kick Member

```csharp
public bool KickMember(CSteamID memberId);
```

Marks the ID as a member that should be removed from the lobby. This simply sets the ID to a "kick list" on the lobbies metadata and will cause the EventLobbyAskedToLeave event to be raised for the effected user on the event is present on the [Matchmaking](../api/matchmaking.md) interface and [Lobby Manager](../unity/components/lobby-manager.md).

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
public string GetMemberMetadata(LobbyMemberData member, string key);
```

Gets the metadata field for the indiacated user
