---
description: Code free drag and drop quick match style session lobby tool
---

# Quick Match Lobby Control

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Create a session [lobby ](../../../../company/steam/steamworks/multiplayer/matchmaking-tools.md)and manage a quick match style UI with ZERO code required.

Quick match based lobbies are the simplest and cleanest user experience for your player in common game design. They present very little to no real UI elements concerned with the "lobby" rather the user or system defines the search arguments and searches for or creates a new session to match players with. This approach requires the least amount of input from players typically reducing match wait types by using more flexible search parameters when needed.

### DOTA 2 Example

![](<../../../../.gitbook/assets/image (1) (2).png>)  ![](<../../../../.gitbook/assets/image (4) (4).png>)

Screen captures of DOTA 2 "Play DOTA" option is a true example of Steam Lobby used for Quick Match matchmaking. The player hits one button, optionally selects preferences like ranked vs unranked and the system does the rest based on the player's stats, rather or not they are in a party, geo location, rankings, etc.

### Halo Infinite Example

![](<../../../../.gitbook/assets/image (2) (1) (3).png>)  ![](<../../../../.gitbook/assets/image (5) (1) (3).png>)

Screen captures of Halo Infinite's "Quick Play" option is a prime example of a Quick Match Lobby setup. The player hits one button and the system will find an appropriate match based on the player's stats, rather or not they are in a party, geo location, rankings, etc.

## Features

### Authentication

Automatically checks the VAC and auth status of connecting user's asking user's to leave if they fail the checks you have configured.

### Simple Quick Match

Search for a match and join, if none is found create a match and wait. Quick match is one of the best options for a quality user experience in most session based multiplayer games. The Quick Match Lobby Control's main function is this, your user's with a single push of a button will be placed in a match with any party they may have as quickly as possible with as little input required as possible.

### Event Driven

Optional Unity Events are available in editor and in code to help you drive additional UI and game logic based on Quick Match status change.

### Working Status

A simple \`Status\` enum is available for use cases where Event Driven is not desired or possible. You can test the \`WorkingStatus\` of the control to see when its idle, searching, waiting or starting.

### Easy Access

Easily access critical information about your Quick Match session for a simple and efficient integration with any networking HLAPI you would like. Quickly access the lobby, owner, the local user's member and much more.

## Prefab

A production ready prefab is available and configured with the features displayed above. You can see an example of this prefab in use in the [Quick Match Example](../../unity-engine/sample-scenes/lobby/#quick-match-example) scene.

<figure><img src="../../../../.gitbook/assets/image (3) (1) (5).png" alt=""><figcaption></figcaption></figure>

## Events

### Evt Process Started

```csharp
public UnityEvent evtProcessStarted;
```

This event is invoked when the system starts the process of quick matching and can be used to trigger other game logic that should happen when the process starts.

### Evt Process Stopped

```csharp
public UnityEvent evtProcessStopped;
```

This event is invoked when the system stops the process of quick matching such as from a cancel and can be used to trigger other game logic that should happen when the process stops.

### Evt Lobby Full

```csharp
public LobbyDataEvent evtLobbyFull;
```

This event is invoked when the lobby becomes full e.g. all available slots are populated with users. This is usually used to start whatever your networking API requires to start a network session.

### Evt Game Created

```csharp
public GameServerSetEvent evtGameCreated;
```

This event is invoked when the owner calls Lobby.SetGameServer() or uses the SetGameServer methods on the Quick Match Lobby Controller. This indicates to all members that the network session is ready for them to connect to it.

### Evt Enter Success

```csharp
public LobbyDataEvent evtEnterSuccess;
```

This event is invoked when the user joins or creates a lobby e.g. lets you know the local user is now in a session lobby.&#x20;

### Evt Enter Failed

```csharp
public LobbyResponceEvent evtEnterFailed;
```

This event is invoked when the user attempted to join an existing lobby but for some reason it failed. The event parameter will indicate what went wrong.

### Evt Created Failed

```csharp
public EResultEvent evtCreatedFailed;
```

This event is invoked when the the user attempted to create a new lobby but for some reason it failed. The event parameter will indicate what went wrong.

### Evt State Changed

```csharp
public UnityEvent evtStateChanged;
```

This event is frequently invoked, and will trigger when any data change happens such as user's coming and going, authentication failing, etc. This can be used to drive general game logic that simply needs to know when to check the system for a change.

## Fields and Attributes

### Idle Group

```csharp
public GameObject indelGroup;
```

This game object is enabled when the system is \*\*NOT\*\* processing. This is useful to place a "Play Button" or similar elements in that you want to be "turned off" when the system starts processing. You can similarly use the \`Evt Process Started\` event to control you UI

### Processing Group

```csharp
public GameObject processingGroup;
```

This game object is enabled when the system \*\*IS\*\* processing. This is useful to place a "status message" object in that should be displayed when the system is working.

### Update Rich Presence Group Data

```csharp
public bool updateRichPresenceGroupData;
```

Indicates rather or not the system could update the player's \`steam\_player\_group\` and \`steam\_player\_group\_size\` rich presence data.

### Kick When

```csharp
public EAuthSessionResponce[] kickWhen;
```

A collection of authentication response codes that if seen on authentication the user should be asked to leave.

### SearchArguments

```csharp
public SearchArguments searchArguments;
```

Used with any form of search performed through the Lobby Manager including the [Search](quick-match-lobby-control.md#search) and [QuickMatch ](quick-match-lobby-control.md#quick-match)methods. This is used to define the "search arguments" e.g. the rules to be tested when searching for lobbies.

The `SearchArguments` data type is an internal class:

```csharp
[Serializable]
public class SearchArguments
{
    /// <summary>
    /// If less than or equal to 0 then we wont use the open slot filter
    /// </summary>
    public int slots = -1;
    public ELobbyDistanceFilter distance = ELobbyDistanceFilter.k_ELobbyDistanceFilterDefault;
    public List<NearFilter> nearValues = new List<NearFilter>();
    public List<NumericFilter> numericFilters = new List<NumericFilter>();
    public List<StringFilter> stringFilters = new List<StringFilter>();
}
```

The fields of the class are as follows

* slots\
  If less than or equal to 0 this will be ignored otherwise this will indicate the number of available slots resulting lobbies must have. For example if you wanted to find a lobby for you and 3 friends then you would provide a value of 4 in this field to return only lobbies that had 4 open slots.
* distance\
  An enumerator that indicates the max alowed distance between the searching user and the members of the resulting lobbies. For more details on the values see [Valve's documentation on ELobbyDistanceFilter](https://partner.steamgames.com/doc/api/ISteamMatchmaking#ELobbyDistanceFilter), in summary
  * Close\
    Only in the same Valve region as this user
  * Default\
    In the same or near by Valve region as this user
  * Far\
    Up to half a world away&#x20;
  * World Wide\
    No filtering at all
* nearValues\
  Key value pairs that the system should search for "near by" values for. See [Valve's documentation](https://partner.steamgames.com/doc/api/ISteamMatchmaking#AddRequestLobbyListNearValueFilter) on this feature for more details. In summary this doesn't "filter out" lobbies but rather effects the sorting, the closer a lobby's metadata is to matching this value the higher it will be sorted in the resulting list. This is useful for say "Player Rank" whose min and max player rank is as near the player's actual rank as possible. To do this you could set near values of `minRank = myRank` and `maxRank = myRank` this would not exclude any lobbies in and of its self but would sort lobbies such that top results where nearest "my rank" ... this assumes minRank is the rank of the lowest ranked player in that lobby and maxRank is the rank of the highhest ranked player in that lobby
* numericFilters\
  Instructs the search to perform a numeric filtering operation on these fields and can filer by the following methods
  * Equal to or Less than
  * Less than
  * Equal
  * Greater than
  * Equal to or Greater thhan
  * Not Equal
* stringFilter\
  Instructs the search to perform a string filtering operation on these fields and can be filtered by the same methods as numeric filters. Valve doesn't explain what the result of each is so test to confirm desired results.

### CreateArguments

```csharp
public CreateArguments createArguments;
```

Used by the Lobby Manager any time a lobby is created with it, this would apply to [Create ](quick-match-lobby-control.md#create)as well as [QuickMatch ](quick-match-lobby-control.md#quick-match)when no lobby is found and create on fail is set to true.

The `CreateArguments` data type is an internal class:

```csharp
[Serializable]
public class CreateArguments
{
    public string name;
    public int slots;
    public ELobbyType type;
    public List<MetadataTempalate> metadata = new List<MetadataTempalate>();
}
```

the fields of the class are as follows

* name\
  This will be set as metadata on the lobby when created e.g. \
  `MyLobby["name"] = value;`
* slots\
  This is the maximum number of slots this lobby will have ... this is including the owner of the lobby.
* type\
  The type of lobby to create, you can learn more about the [available types above](quick-match-lobby-control.md#lobby-types).
* metadata\
  Metadata fields to be set on the lobby once created. This is a simple string key and string value pairing. Metadata is what is used when "filtering" or "searching" for lobbies.

### Lobby

```csharp
public Lobby Lobby { get; set; }
```

The lobby the manager is currently managing. This will automatically be updated when you use the lobby manager to create, join or leave a lobby. If you create, join or leave a lobby from outside the manager then you should update this field accordingly.

### Owner

```csharp
public LobbyMember Owner => get;
```

Gets the [Lobby Member](../../data-layer/lobby-member-data.md) data for the current lobby owner.

### Me

```csharp
public LobbyMember Me => get;
```

Gets the local user's [Lobby Member](../../data-layer/lobby-member-data.md) data for the current lobby.

### HasLobby

```csharp
public bool HasLobby => get;
```

True if the manager is managing a lobby, false otherwise.

### Searching

```csharp
public bool Searching => get;
```

True if the system is searching for a match at the moment.

### IsPlayerOwner

```csharp
public bool IsPlayerOwner => get;
```

True if the local user is the owner of the managed lobby, false otherwise.

### AllPlayersReady

```csharp
public bool AllPlayersReady => get;
```

True if all members of the lobby have marked them selves as ready, otherwise false.

### IsPlayerReady

```csharp
public bool IsPlayerReady { get; set; }
```

Returns true if the player has marked them self as ready on this lobby. This can be set to mark the player as ready or not on this lobby.

### Full

```csharp
public bool Full => get;
```

Returns true if the lobby is currently full, false otherwise.

### Slots

```csharp
public int Slot => get;
```

How many people can join this lobby if any lobby at all

### Member Count

```csharp
public int MemberCount => get;
```

How many people are currently in this lobby if any lobby at all

### Game Server

```csharp
public LobbyGameServer GameServer => get;
```

The current game server set by the owner of the lobby if any

### Working Status

```csharp
public Status WorkingStatus => get;
```

The current status of the system

* Idle\
  Not processing
* Searching\
  If currently searching for a match
* Waiting For Start\
  Match found but lobby not full and session not started
* Starting\
  Match found and lobby is now full  ... the owner should be starting up the network session

### Timer

```csharp
public float Timer => get;
```

The amount of time since the process started.

## Methods

### Cancel

```csharp
public void Cancel();
```

Stops the process of searching and if in a lobby exits the lobby

### Run Quick Match

```csharp
public void RunQuickMatch();
```

Starts the process of searching for and or creating a session lobby as required.

### Set Game Server

```csharp
public void SetGameServer();
public void SetGameServer(string address, ushort port, CSteamID gameServerId);
public void SetGameServer(string address, ushort port);
public void SetGameServer(CSteamID gameServerId;
```

This can only be called by the owner of the lobby and should be called when the network session is ready for the members to connect to it.&#x20;

If no parameter is passed in

```csharp
SetGameServer();
```

The system will assume that the owner of the lobby is the server e.g. a P2P session where the lobby owner is the "Host"

All other overloads require you to indicate what the connection information is for the session.
