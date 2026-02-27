# Lobby

Steam Lobbies are often misunderstood as multiplayer or networking features. In reality, they are chat rooms with metadata, so much so that Valve refers to them internally as “chats” rather than “lobbies.”

At their core, Steam Lobbies provide a way to group players and associate metadata with both the group (the lobby) and its members. This metadata enables lobby searching, matchmaking, and player-specific state sharing, all without requiring a direct network connection between players.

Steam’s matchmaking system is built on top of this lobby structure. A lobby acts as a shared space where data about the session (e.g., game mode, map, status) is stored as key-value pairs. Each player also stores personal metadata (e.g., loadout, readiness) visible only to other lobby members.

To summarise:

* **Lobby metadata** communicates session-wide information. It is public to anyone who can see or search for the lobby.
* **Member metadata** communicates per-player information. It is only accessible to other members within the same lobby.

If you’re implementing party-based play, session finding, or similar functionality, Steam Lobbies are likely what you’re looking for.

For further technical details, refer to Valve’s [Steamworks Documentation on Matchmaking](https://partner.steamgames.com/doc/features/multiplayer#matchmaking).

## What _is_ a Lobby?

The most important thing to understand: **a Steam Lobby is not a networking system**.

* You can join and use a lobby with no network session active.
* You can establish network connections without ever using a lobby.
* The two systems are entirely independent.

Think of a Steam Lobby as a structured chat room with metadata. It helps players group up and exchange lightweight information, such as session intent, player loadouts, or status, before initiating an actual multiplayer session.

Steam Lobbies are commonly used as the first step in forming a party, and later as the container for matchmaking data. But the lobby itself does **not** facilitate multiplayer gameplay. That’s your job, through your networking layer.

Your user can be a member of more than 1 lobby. Steam allows users to be a member of 1 (Normal) lobby and up to 2 (Invisible) lobbies. It would be typical that a game would be managing at least 2 lobbies for a player.

### Lobby Type

<table><thead><tr><th width="120">Type</th><th width="116">Steam Class</th><th width="151">Visibility</th><th width="150">Join Method</th><th>Common Use Case</th></tr></thead><tbody><tr><td><strong>Private</strong></td><td>Normal</td><td>Hidden from friends &#x26; searches</td><td>Only by direct invitation</td><td>Closed sessions with specific players (e.g., invite-only co-op).</td></tr><tr><td><strong>Friends Only</strong></td><td>Normal</td><td>Visible to friends only</td><td>By friends or by invitation</td><td>Drop-in games for friends, no public exposure.</td></tr><tr><td><strong>Public</strong></td><td>Normal</td><td>Visible to all via search &#x26; friends list</td><td>Open or invite</td><td>Public matchmaking sessions.</td></tr><tr><td><strong>Invisible</strong></td><td>Invisible</td><td>Searchable, but hidden from the friends list</td><td>Open or invite</td><td>Hidden lobbies that can be searched, but don’t appear as “playing with friends.” Useful for matchmaking where friends list exposure is undesired.</td></tr></tbody></table>

### Session Lobby

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

This is just a regular Steam Lobby used in a particular way.

A **Session Lobby** is the term used for the lobby where matchmaking takes place, typically used to prepare a game session. In games like _DOTA_, _Halo_, or similar titles, this is the lobby you enter after clicking "Play." It is the space where players are matched with others either randomly or based on specific criteria, and it serves as the gateway to entering a game session.

In a **Session Lobby**, players are typically grouped for matchmaking purposes. The lobby enables random or pre-set players to find each other and organise the session, such as determining the game mode, map, or other preferences before the actual game starts. This is where the matchmaking process occurs, facilitating the connection between players who may not know each other but want to play together.

Key functions of a **Session Lobby** include:

* **Matchmaking:** Finding and joining players with similar criteria or skill levels.
* **Session preparation:** Players can view game settings, such as map and mode, and confirm before entering the match.
* **Random or structured grouping:** Players may be matched randomly or as part of a more controlled, structured system, depending on the game’s matchmaking rules.

The **Session Lobby** is critical for enabling multiplayer games where players do not know each other beforehand, providing the infrastructure for matchmaking and game session preparation.

### Party Lobby

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

This is just a regular Steam Lobby used in a particular way.

A **Party Lobby** is a term commonly used to describe a lobby where friends or players can group before entering a session. It serves as a way for players to coordinate and share information about which session lobby to join together, but it is **not** used to create or host games directly.

In games like _DOTA_ or _Halo_, the **Group Lobby** functions similarly to a "Fire Team" or "Party." Players in a group lobby do not initiate a game directly. Instead, they use the lobby to gather, share information, and coordinate on which game session they want to join. Once the group decides on a session, they transition into the appropriate **Session Lobby** for the actual gameplay.

Party lobbies are typically used for:

* Organising friends or teammates to play together.
* Sharing session details like the Lobby ID or Game Server ID, or similar, they intend to join.
* Ensuring that all group members are on the same page before joining a session.

While a **Party Lobby** doesn’t facilitate the creation of a game, it’s essential for games that want to manage the social aspect of matchmaking and ensure a smooth transition into the gameplay experience.

### General Lobby

This is simply a lobby that is neither a "Session" lobby nor a "Party" lobby. Steam Lobby can be used for any number of things; it is effectively just a chat room with metadata.

### Members

Each user in a lobby is represented as a **Lobby Member**. Every member can attach a set of metadata to themselves, key-value pairs visible to other members of the same lobby. This metadata can only be set by the member it belongs to.

* You can **read** every other member's metadata.
* You can **only write** your own.

This data is not visible outside the lobby. If you're not a member, you cannot access the member metadata. It’s often used to communicate things like player loadout, readiness status, or role selection within the session.

### Metadata

**Lobby metadata** and **member metadata** are the foundation of how Steam Lobbies are used for matchmaking and session setup.

All metadata is stored as key-value pairs, where both the key and value are strings:

```csharp
Dictionary<string, string>
```

**Lobby Metadata**

* Set by the **lobby owner (host)**.
* Readable by **anyone who can see the lobby**, including search results.
* Used to describe the session: map name, game mode, rules, etc.
* Used by the matchmaking system to **filter and sort search results**.

**Member Metadata**

* Set by the **individual member**.
* Readable only by **other members** of the same lobby.
* Used to describe player-specific info: loadout, readiness, team choice, etc.

### Chat

Despite being called a **Lobby** in the public-facing Steam API, on Valve’s backend, it's referred to as a **chat room** — because that's what it is under the hood.

**Core Concepts**

* A Steam Lobby **is a chat room** with built-in metadata and structured membership.
* You can **send and receive messages** between lobby members **without a network connection**.
* This system is separate from your game’s networking — it’s Steam-to-Steam communication.

**Message Format**

Lobby chat messages are sent as raw `byte[]` data. It’s up to your game to define what that data represents — e.g. plain text, JSON, binary instructions, etc.

* Messages are only delivered to current **members** of the lobby.
* There’s **no built-in guarantee of order, delivery, or reliability** — treat it as lightweight messaging.
* Ideal for session coordination like ready checks, map voting, or status updates before starting a match.

**Use Cases**

* Displaying lobby chat text in a UI.
* Exchanging ready/check-in states.
* Syncing small pre-match data (e.g. character selections).

For structured handling of this feature, consider implementing a **Lobby Chat Director** system in your game to route and interpret messages.

## Examples

### Member of

You will often need to Get the current General, Session or Party lobby your player is in. We provide easy tools for doing this.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.

<figure><img src="../.gitbook/assets/image (412).png" alt=""><figcaption></figcaption></figure>

### Load

The load field lets you automatically load a lobby you are a member of into this component.

* Any\
  Simply gets the first lobby the player is a member of regardles of its type
* General\
  Gets the first "general" type lobby the player is a member of
* Session\
  Gets the first "session" type lobby the player is a member of
* Party\
  Gets the frist "party type lobyb the player is a member of

## C\#

```csharp
// You can iterate over all lobbies your player is a member of with
foreach (var lobby in LobbyData.MemberOfLobbies)
{
}

// We have also created short cuts for Session
if(LobbyData.SessionLobby(out var lobby))
{
}

// And for Party
if (LobbyData.PartyLobby(out var lobby))
{
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
USteamToolsSubsystem* SteamTools = USteamToolsSubsystem::GetSteamToolsSubsystem();
if (!SteamTools)
{
    UE_LOG(LogTemp, Warning, TEXT("SteamToolsSubsystem not initialized"));
    return;
}

// Access the MemberOfLobbies array
const TArray<int64>& Lobbies = SteamTools->MemberOfLobbies;

// Example: log the lobby IDs
for (int64 LobbyId : Lobbies)
{
    UE_LOG(LogTemp, Log, TEXT("Member of Lobby: %lld"), LobbyId);
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Create

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

<figure><img src="../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

Creation settings can be made party-wise and configured for General, Session or Party type lobbies.

<figure><img src="../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

### Party Wise

If true, the system will intelligently update party and session lobbies. For example, if you are at a Party and attempt to create a Session, the system will first check if you are the Party leader; if so, it will create the lobby and then notify the party of that lobby so that your party members can join.&#x20;

### Usage Hint

This tells our system what your intended use is for this lobby: will it be "General", meaning Party Wise logic doesn't apply, or will it be a Session or Party type lobby where the Party Wise logic will apply.

### Slots

This is the maximum number of people (including yourself) that the lobby can handle.&#x20;

### Type

The Steam type of lobby

* Private\
  Players can only join by invitation. Note if you're in a party and this is a session, the system will invite each party member on creation, but will not set the z\_heathenSessionLobby metadata on the party lobby
* Friends Only\
  Only friends will be allowed to query for this lobby; non-friends can still be directly invited.
* Public\
  This lobby will appear in lobby search and can generally be joined by anyone, assuming available slots and no Steam Social blocks.
* Invisible\
  This lobby is available for anyone to join, but will not appear in search; this is typically only used for Party use lobbies.

## C\#

```csharp
// Generic Create Function where you pass in an enumerator to set the type
ELobbyType type; //= Set the type of lobby you want
int slots;       //= Set the number of members this lobby can have
LobbyData.Create(type, slots, HandleLobbyCreate);

// This assumes you want to create an Invisible lobby for use as a Party lobby
LobbyData.CreateParty(slots, HandleLobbyCreate)

// This assumes you want a Public lobby type for use as a Session lobby
LobbyData.CreatePublicSession(slots, HandleLobbyCreate)

// This assumes you want a Private lobby type for use as a Session lobby
LobbyData.CreatePrivateSession(slots, HandleLobbyCreate)

// This assumes you want a Friend Only lobby type for use as a Session lobby
LobbyData.CreateFriendOnlySession(slots, HandleLobbyCreate)
```

All options take a function as the last parameter to be called when the process is complete. The function takes the form of.

```csharp
void HandleLobbyCreate(EResult result, LobbyData lobby, bool ioError)
{
    //This is called when creation is completed
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (202).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// You will need to declare your callback such as 
CCallResult<YourClassName, LobbyCreated_t> m_LobbyCreate_t;

// Then call create lobby which will return a SteamAPICall_t handle that can be used
// to set the m_LobbyCreate_t callback.
SteamAPICall_t handle = SteamMatchmaking()->CreateLobby(static_cast<ELobbyType>(type), maxMembers);
m_LobbyCreate_t.Set(handle, this, &YourClassName::SteamCallback);

// The SteamCallback is a function that will be invoked by the callback
YourClassName::SteamCallback(LobbyCreated_t* Response, bool bIOError)
{
	// Unreal runs callbacks on a seperate thread so you may need to dispatch the result
	// to your game thread 
	FGraphEventRef GameThreadTask = FFunctionGraphTask::CreateAndDispatchWhenReady([this, bIOError, Response]()
		{
			if (!bIOError)
			{
			
				// Callback in this context would simply be a delegate on your game thread
				if (Callback.IsBound())
					Callback.Execute(static_cast<UEResult>(Response->m_eResult), static_cast<int64>(Response->m_ulSteamIDLobby));
			}
			else
			{
				if (Callback.IsBound())
					Callback.Execute(UEResult::EPC_IOFailure, 0);
			}
		}, TStatId(), nullptr, ENamedThreads::GameThread);
	GameThreadTask->Wait();

	delete this;
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Search

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Use the Lobby Search component to search for and display found lobbies to your UI.

<figure><img src="../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

### Party Wise

The party-wise flag informs the system to respect party logic when searching for and,, joining a lobby. For example if you are the party leader the system will automatically search for lobbies that have enough open slots for you and your party.

### Slots

The number of open slots required, if the value is 0 then it will be excluded from searching many any non-full lobby found will be returned. If you are in a party and using Party Wise this will be set on search to the number of people in your lobby.

### Distance

Using Steam Distance Filter options how far afield should we search for lobbies?

* Close\
  Only lobbies in the same region as the player
* Default\
  Lobbies in the same or adjacent regions
* Far\
  Distant lobbies will be permitted but not "global"
* Worldwide\
  We will not filter on distance at all and will consider all lobbies available.

### Near Values

<figure><img src="../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

Used when searching to sort the results. This will check for lobbies with the indicated key in their metadata, if found it will attempt compare the value with the value entered here. This should be a numeric value for the best results. For example you can search for all lobbies where matchRank is near 10. The result would be that lobbies with matchRank 9 and 11 would appear higher in the result list than lobbies with matchRank 5 or 15.

### Numeric Filters

Similar to Near Values however this will be used to include/exclude results from the list entirely

<figure><img src="../.gitbook/assets/image (130).png" alt=""><figcaption></figcaption></figure>

### String Filters

Include or exclude records based on string valued metadata e.g. does a map name match for example.

<figure><img src="../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

### Max Results

{% hint style="success" %}
&#x20;Steam will —Never— return more than 50 entries.

A Steam Lobby is —Not— a game server and the Steam can —Not— be used to list every lobby available.&#x20;

Steam Lobby —Is— a matchmaking system, ideal for returning the 1 optimal lobby that the player should join given the filters specified.   &#x20;

Search results are always priority filtered such that the nearest, oldest, most full lobby that satisfies your custom filters will be listed first.
{% endhint %}

How many entries should be returned at maximum.&#x20;

### Template

The object that will be spawned for each lobby found. This uses the Lobby component to display results.

<figure><img src="../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

### Content

Where entries will be parented when spawned.

## C\#

```csharp
public void SearchForLobbies()
{
    // First, define your search arguments
    SearchArguments args = new();
    args.distance = ELobbyDistanceFilter.k_ELobbyDistanceFilterDefault;
    args.stringFilters.Add(new() { key = "SomeKey", value = "SomeValue", comparison = ELobbyComparison.k_ELobbyComparisonEqual });

    // Next use them ... in this case, we use expression 
    LobbyData.Request(args, 1, (Lobbies, IOError) =>
    {
        // Lobbies is an array of lobbies that were found
        // IOError is true if there was some error
    });
    // Or you can use a named function
    LobbyData.Request(args, 1, HandleResults);
}

private void HandleResults(LobbyData[] Lobbies, bool IOError)
{
    // Lobbies is an array of lobbies that were found
    // IOError is true if there was some error
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

First you must define your filter arguments; you must do this before each request for a lobby list. Each time you request the lobby list, the current filters are cleared.

<figure><img src="../.gitbook/assets/image (333).png" alt=""><figcaption></figcaption></figure>

Next, we request the lobby list. Typically, you would simply check if you found any/1 and if so, join the first one. But if you wanted to "browse", you can iterate over up to 50 lobbies,

<figure><img src="../.gitbook/assets/image (335).png" alt=""><figcaption></figcaption></figure>

Note that it is not possible to return "all" lobbies; Steam Lobby is meant for matchmaking, not server browsing. Please see the [Steam Game Server](steam-game-server.md) for more information on browsing servers.

## C++

```cpp
// Lobby Filter features
// Distance
ELobbyDistanceFilter filter = ELobbyDistanceFilter::k_ELobbyDistanceFilterDefault;
SteamMatchmaking()->AddRequestLobbyListDistanceFilter(filter);

// Slots Available
int32 slotsAvailable = 4;
SteamMatchmaking()->AddRequestLobbyListFilterSlotsAvailable(slotsAvailable);

// Near Value
const ANSICHAR* Key = "SomeKey";
int32 ValueToBeCloseTo = 42;

SteamMatchmaking()->AddRequestLobbyListNearValueFilter(Key, ValueToBeCloseTo);

// Numerical 
const ANSICHAR* Key = "PlayerCount";
int32 ValueToMatch = 4;

// Assume "greater than or equal"
ELobbyComparison Comparison = ELobbyComparison::k_ELobbyComparisonEqualToOrGreaterThan;

SteamMatchmaking()->AddRequestLobbyListNumericalFilter(
    Key,
    ValueToMatch,
    Comparison
);

// Result Count
int32 maxResults = 50;
SteamMatchmaking()->AddRequestLobbyListResultCountFilter(maxResults);

// String 
const ANSICHAR* Key   = "GameMode";
const ANSICHAR* Value = "Hardcore";

ELobbyComparison Comparison = ELobbyComparison::k_ELobbyComparisonEqual;

SteamMatchmaking()->AddRequestLobbyListStringFilter(
    Key,
    Value,
    Comparison
);

// As with any Callback you first need to have declared the callback, usually as a
// property of your class
CCallResult<YourClassName, LobbyMatchList_t> m_LobbyMatchList_t;

// When you're ready to request the list 
SteamAPICall_t handle = SteamMatchmaking()->RequestLobbyList();
m_LobbyMatchList_t.Set(handle, this, &YourClassName::SteamCallback);

// The callback handler
void YourClassName::SteamCallback(LobbyMatchList_t* Response, bool bIOError)
{
	// Unreal runs callbacks on a thread, so if needed, invoke to GameThread
	// Callback in this case is assumed to be a delegate on your game thread
	FGraphEventRef GameThreadTask = FFunctionGraphTask::CreateAndDispatchWhenReady([this, bIOError, Response]()
		{
			if (!bIOError)
			{
				if (Callback.IsBound())
					Callback.Execute(Response->m_nLobbiesMatching);
			}
			else
			{
				if (Callback.IsBound())
					Callback.Execute(0);
			}
		}, TStatId(), nullptr, ENamedThreads::GameThread);
	GameThreadTask->Wait();

	delete this;
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Join

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

<figure><img src="../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

With Join added you can now join a target lobby easily and optionally have the operation be "Party Wise"

<figure><img src="../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

With the Join feature added you can join a lobby by its ID, either by typing in the code you want to join (useful in dev testing)

<figure><img src="../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

or by having it read from an Input Field

<figure><img src="../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure>

You can also connect Lobby components to Lobby List entries so that a given lobby is joined and updated in a particular component

<figure><img src="../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>

This is demonstrated in the Demo Scene where each Lobby Entry in the Lobby Search has a "join Button" when clicked it calls the "Request join" of the Steam Lobby UI so that the user joins the listed lobby updating the UI for that lobby on join.

## C\#

```csharp
public void JoinLobby(LobbyData lobby)
{
    // You can simply call Join and provide the callback as expression
    lobby.Join((Result, IOError) =>
    {
        // Result.Lobby is the lobby joined if any
        // Result.Response to the response message, if any
        // Result.Locked is this lobby locked?
    });
    // Or feed it a named function
    lobby.Join(HandleJoined);
}

private void HandleJoined(LobbyEnter Result, bool IOError)
{
    // Result.Lobby is the lobby joined if any
    // Result.Response to the response message, if any
    // Result.Locked is this lobby locked?
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

You can join a lobby given its ID as either a Hex String or the int64 ID of the lobby, such as from a Request Lobby List.

<figure><img src="../.gitbook/assets/image (336).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// Have a property to hold your callback
CCallResult<YourClassName, LobbyEnter_t> m_LobbyEnter_t;

// When you call JoinLobby use the handle on your callback
CSteamID lobbyId;
SteamAPICall_t handle = SteamMatchmaking()->JoinLobby(lobbyId);
m_LobbyEnter_t.Set(handle, this, &YourClassName::SteamCallback);

// The callback will be invoked when complete
void YourClassName::SteamCallback(LobbyEnter_t* Response, bool bIOError)
{
	// Unreal runs callbacks on its own thread so, you may need to dispatch to 
	// game thread.
	// This assumes Callback is a delegate on your game thread.
	FGraphEventRef GameThreadTask = FFunctionGraphTask::CreateAndDispatchWhenReady([this, bIOError, Response]()
		{
			if (!bIOError)
			{
				if (Callback.IsBound())
					Callback.Execute(static_cast<int64>(Response->m_ulSteamIDLobby), Response->m_bLocked, static_cast<UEChatRoomEnterResponse>(Response->m_EChatRoomEnterResponse));
			}
			else
			{
				if (Callback.IsBound())
					Callback.Execute(0, true, UEChatRoomEnterResponse::EPC_Error);
			}
		}, TStatId(), nullptr, ENamedThreads::GameThread);
	GameThreadTask->Wait();

	delete this;
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Leave

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

The leave feature doesn't expose any new inspector fields but does enable the Leave call which can be accessed from Unity event such as a button click.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
public void LeaveLobby(LobbyData lobby)
{
    lobby.Leave();
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (337).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// When manually leaving a lobby, update the Steam Tools Subsystem
// to keep local lobby membership state accurate.
USteamToolsSubsystem* SteamToolsSubsystem = USteamToolsSubsystem::GetSteamToolsSubsystem();
if (!SteamToolsSubsystem)
{
    UE_LOG(LogTemp, Warning, TEXT("SteamToolsSubsystem not initialized"));
    return;
}

const uint64 LobbyIdValue = LobbyId.ConvertToUint64();

// Remove from locally tracked lobbies
SteamToolsSubsystem->MemberOfLobbies.Remove(LobbyIdValue);

// Leave the Steam lobby
SteamMatchmaking()->LeaveLobby(LobbyId);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Invite to Lobby

Invite a friend to join a specific lobby. It is important to understand that when inviting a friend, they may not accept right away. You can invite friends who are not currently playing the game or may not even own the game. See the [Accept Lobby Invite](lobby.md#accept-lobby-invite) for details on how to handle all the use cases your accepting user might face.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

As with leave there are no new inspector fields but you can now access several invite options from Unity Actions such as button clicks.

#### From String

Invite a user by passing in the Hex ID this is handy for dev testing

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

#### From Input

Or you can read that ID from an input field so players can type a friend's Steam Hex ID in to invite them directly.

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

#### From User

You can also, of course, invite a given [User](user.md) component, such as those listed in your [friend's list component](user.md#friend-list).

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
public void InviteToLobby(UserData User, LobbyData Lobby)
{
    // From the user
    User.InviteToLobby(Lobby);
    // Or, from the Lobby
    Lobby.InviteUserToLobby(User);
}
```

Alternatively, you can open the Steam Overlay to the Lobby Invite Dialogue and select a user to invite from there.

```csharp
Overlay.Client.ActivateInviteDialog(Lobby);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Inviting a user to a lobby is a simple node.

<figure><img src="../.gitbook/assets/image (338).png" alt=""><figcaption></figcaption></figure>

The user, if they are in-game, will get the Lobby Invite event raised; you can listen to this event from the Steam Game Instance.

<figure><img src="../.gitbook/assets/image (339).png" alt=""><figcaption></figcaption></figure>

The user will also receive the invite in their friend chat and can accept from there. If they did toggle ot the friend chat and accept from there while in game then the Join Requested event will be raised.

<figure><img src="../.gitbook/assets/image (340).png" alt=""><figcaption></figcaption></figure>

They can also receive and accept invites when they are not in-game via the friend chat. If this happens, then the game will be launched with the lobby ID on the command line. You can get the lobby ID from the command line with this:

<figure><img src="../.gitbook/assets/image (341).png" alt=""><figcaption></figcaption></figure>

If this returns 0 then no invite lobby was on the command; if it is not 0 then that indicates the user accepted an invite and that is what launched the game, so logically, you should load the game in to the proper state and then join the indicated lobby.

## C++

```cpp
CSteamID lobbyId;
CSteamID userID;
SteamMatchmaking()->InviteUserToLobby(lobbyId, userId);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Accept Lobby Invite

When a lobby invite is sent to a user, a number of things happen:

* The user will get a notification in Steam Friend Chat with an Accept button they can click
* If the user is in a game, they will receive the "Lobby Invite" event.

***

If the user clicks the "Accept" button from the Steam Friend chat, a few different things can happen.

{% hint style="success" %}
Understand that when a user clicks "Accept", that user is NOT joined to the lobby. It simply notifies the game that the user has accepted an invite. It is then up to the game logic to join said lobby.
{% endhint %}

* If the user is not currently playing the game, Steam will launch the game with the lobby ID on the command line.
* If the user is currently playing the game, the "Game Lobby Join Requested" event will be raised.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

### General Events

The recommended approach, add a General Events setting and use the Lobby Invite Received or Lobby Join Requested events.

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

* Lobby Invite Recieved\
  This is raised when the invite is sent, you can handle this event to show a UI element wher the player can review who sent the invite and optionally accept the invite.
* Lobby Join Requested\
  This is raised when the "Accept" button is clicked in the Steam Friends Chat UI. Steam will show the lobby invite in the user's chat with an accept button. Keep in mind that this button could be pressed well after the invite was sent so you should be prepared to handle an invite or missing lobby.

### Join On Invite

This can be used to automatically join when an invite is received. In general this is not a good practice but is useful in some cases.

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

With the Join On Invite settings added, the Join settings will also be added and this will allow you to configure how the system should respond to lobby invites.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Party Wise

This will cause the system to respect party logic when accepting an invite and driven by the [Join](lobby.md#join) settings.

### Mode

Steam Lobby Invite is a 2 step process and our system can join at either step.

* With Inital Invite\
  When you first send the invite before the player has seen it in their Friend Chat UI Steam will notify the Steamworks SDK. We can respond to that invite and join immediatly. This is not generally recommended but can be useful in some cases.
* After Accept In Friend Chat\
  Steam will show the invite in the receiving user's Friend Chat along with an "Accept" button. When that button is clicked we can respond to that.

### Filter

This will ignore invites if the user is currently a party, session or any lobby depending on the configuration.

### Preprocess

This will happen before joining the target lobby and can be used to first leave any existing lobby, session lobby or party lobby.

## C\#

If you want to handle the invite process entirely within the game, then you will want to react to the Lobby Invite event.

```csharp
SteamTools.Events.OnLobbyInvite += HandleLobbyInvite;
```

The handler for this takes the form of:

```csharp
private void HandleLobbyInvite(LobbyInvite Response)
{
    // Response.ForGame the game the invite is for
    // Response.FromUser the user that invited you
    // Response.ToLobby the lobby you were invited to
}
```

Register a handler to listen on the Game Lobby Join Requested event. This event is raised when the user clicks the "Accept" button in the Steam Friend chat after receiving an invite to join a lobby.

```csharp
SteamTools.Events.OnLobbyJoinRequested += HandleLobbyJoinRequest;
```

The handler for this event would look like this:

```csharp
private void HandleLobbyJoinRequest(LobbyData Lobby, UserData User)
{
    // Lobby is the lobby you were invited to
    // User is the user who invited you
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Use the Steam Tools Subsystem to bind an event on the Lobby Join Requested

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

The Lobby ID is the lobby that the player indicated they wish to join.

The User ID is the user who sent the invite that the player accepted.

## C++

```cpp
// In some function of YourClassName
USteamToolsSubsystem* SteamToolsSubsystem = USteamToolsSubsystem::GetSteamToolsSubsystem();
if (!SteamToolsSubsystem)
{
    UE_LOG(LogTemp, Warning, TEXT("SteamToolsSubsystem not initialized"));
    return;
}

// Bind YourClassName::FunctionName to the SteamLobbyJoinRequested delegate
// Make sure FunctionName has the correct signature matching FGameLobbyJoinRequestedCallback
SteamToolsSubsystem->SteamLobbyJoinRequested.AddDynamic(this, &YourClassName::FunctionName);

// This assumes FuncitonName has a signature such as
UFUNCTION()
void FunctionName(int64 LobbyId, int64 UserId); // example
```
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming soon
{% endtab %}
{% endtabs %}

### Detect Lobby on Game Launch

When a user accepts a lobby invite but the game was not running at the time, Steam will launch the game, passing the Lobby ID in on the command line.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

The Command Line option will test the launch parameters from the command line and will invoke the Lobby Join Requested event if the rule is met. You can use this to call [Join](lobby.md#join) or perform similar actions.

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
LobbyData targetLobby = Matchmaking.Client.GetCommandLineConnectLobby();
if(targetLobby.IsValid)
{
    // A lobby was found on the command line. You should join it.
    // when the game is in an appropriate state.
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

If this returns a non-zero value, you have a lobby on the command line.

<figure><img src="../.gitbook/assets/image (167).png" alt=""><figcaption></figcaption></figure>

### C++

Use this as the body of a function that returns the lobby ID ... we use int64 for compatibility with Blueprints, but technically it should be a uint64.

```cpp
FString CmdLine = FCommandLine::Get();
TArray<FString> Tokens;
CmdLine.ParseIntoArray(Tokens, TEXT(" "), true);

for (int32 i = 0; i < Tokens.Num(); ++i)
{
	if (Tokens[i] == TEXT("+connect_lobby") && i + 1 < Tokens.Num())
	{
		int64 LobbyID = FCString::Strtoi64(*Tokens[i + 1], nullptr, 10);
		UE_LOG(LogTemp, Log, TEXT("Lobby Steam ID found: %lld"), LobbyID);
		return LobbyID;
	}
}

UE_LOG(LogTemp, Log, TEXT("No lobby connection parameter found."));
return 0;
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
var args = Environment.GetCommandLineArgs();
ulong value = 0;
for (int i = 0; i < args.Length; i++)
{
    if (args[i] == "+connect_lobby" && i + 1 < args.Length && ulong.TryParse(args[i + 1], out value))
        return value;
}
```
{% endtab %}
{% endtabs %}

### Detect Join/Leave

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

Use General Events and the On User Left and On User Joined events to know when other users come and go.

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
SteamTools.Events.OnLobbyChatUpdate += HandleChatUpdate;
```

The handler takes the form of

```csharp
private void HandleChatUpdate(LobbyChatUpdate_t callback)
{
    UserData who = callback.m_ulSteamIDUserChanged;
    LobbyData whatLobby = callback.m_ulSteamIDLobby;


    if((EChatMemberStateChange)callback.m_rgfChatMemberStateChange == EChatMemberStateChange.k_EChatMemberStateChangeLeft)
    {
        // The user left
    }
    else if ((EChatMemberStateChange)callback.m_rgfChatMemberStateChange == EChatMemberStateChange.k_EChatMemberStateChangeEntered)
    {
        // The user joined
    }
    else if ((EChatMemberStateChange)callback.m_rgfChatMemberStateChange == EChatMemberStateChange.k_EChatMemberStateChangeDisconnected)
    {
        // The user lost connection
    }
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

You can bind the Lobby Chat Update event on the Steam Game State. This tells you what lobby experienced the change, who the change relates to and what change was made. Who made the change will always be the same user, and is there for features like "Kicked" and "Banned" which Valve has access to, but you should never see.

<figure><img src="../.gitbook/assets/image (174).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming soon
{% endtab %}
{% endtabs %}

### Metadata

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add settings:

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Add the Metadata settings, which will let you define metadata that can be set by calling the Set function. You can invoke this from a button press or from General Events on the lobby, such as On Create.

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

The On Changed section lets you track changes to specific metadata keys, these will be invoked anytime the data for the indicated key changes.

## C\#

```csharp
public void MetadataUse(LobbyData Lobby)
{
    // Let's set a simple field to a simple value
    Lobby["a simple field"] = "a simple value";

    // Okay, that was easy, and now let's set that on our member
    LobbyMemberData Me = Lobby.Me;
    Me["a simple field"] = "a simple value";

    // Let's read the owner's metadata
    LobbyMemberData Owner = Lobby.Owner;
    Debug.Log($"Owner's field = {Owner["a simple field"]}");
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Any member of a lobby can get lobby data, but only the owner of the lobby can set the lobby data. Its also possible to loop through all lobby data, though this is not common.

<figure><img src="../.gitbook/assets/image (342).png" alt=""><figcaption></figcaption></figure>

Similar to data on the lobby, each member within the lobby has metadata. Note that you can only set data on your own user, you can read data for any member of the lobby as long as you are also a member of the lobby. It is not possible to read the member data of a lobby you are not a member of.

<figure><img src="../.gitbook/assets/image (343).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}
## C\#

To set metadata

```csharp
CSteamID lobby; // The target lobby
SteamMatchmaking.SetLobbyData(lobby, "SomeKey", "SomeValue")
```

To read metadata

```csharp
CSteamID lobby; // The target lobby
string value = SteamMatchmaking.GetLobbyData(lobby, "SomeKey");
```
{% endtab %}
{% endtabs %}

### Members

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add fields:

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

When you add a Members field&#x20;

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

You get access to the Members Settings

### Show Self

Should the local user aka player, be displayed or should the system skip them and only show other users?

### Template

This is the object that will be spawned for each member in the lobby

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

It should implement the Steam Lobby Member Data component, which will add a [User](user.md) component for you.

### Content

This is simply the game object the records will be spawned under and would typically be a uGUI Layout component.

## C\#

```csharp
public void LoopingLobbyMembers(LobbyData Lobby)
{
    foreach(LobbyMemberData Member in Lobby.Members)
    {
        string MemberName = Member.user.Name;

        Member.user.LoadAvatar(AvatarTexture =>
        {
            // AvatarTexture is now a Texture2D use it well
        });

        string ReadMetadataValues = Member["SomeKey"];
                
        if(Member.IsReady)
        {
            // The member is ready!
        }
        else
        {
            // The member is NOT ready!
        }
    }
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (369).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
// The lobby you want to read for, you must be a member of it for this to work
CSteamID LobbyID; 

int32 Count = SteamMatchmaking()->GetNumLobbyMembers(LobbyID);
TArray<CSteamID> Result;
Result.SetNum(Count);
for (int32 i = 0; i < Count; i++)
{
    Result[i] = SteamMatchmaking()->GetLobbyMemberByIndex(LobbyID, i);
}
```
{% endtab %}

{% tab title="Steamworks.NET" %}
## C\#

```csharp
// Get the member count
int count = SteamMatchmaking.GetNumLobbyMembers(lobby);
// Initalize an array to hold the IDs
CSteamID[] results = new CSteamID[count];

for (int i = 0; i < count; i++)
   results[i] = SteamMatchmaking.GetLobbyMemberByIndex(lobby, i);
```
{% endtab %}
{% endtabs %}

### Notify Ready to Connect

Steam Lobby has a feature called "Game Server" that is used to notify lobby members when there is a game session ready for them to connect to.

{% hint style="success" %}
Yes you use Game Server even if you're working with Listen Server (P2P) networking.

The game server information is simply who or what is serving the game and can be a dedicated server or a player.
{% endhint %}

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (125).png" alt=""><figcaption></figcaption></figure>

You can then add fields:

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Add the Game Server setting;, this will not add any inspector fields but will provide easy-to-use functionality so you can set the Game Server on the lobby.

You can use the "Set Listen Server" feature to indicate that the local user / player is the connection.

{% hint style="success" %}
Listen Server is the proper term for what is sometimes called a "Host" e.g. it is a player that is acting or "listening" as a game server.
{% endhint %}

<figure><img src="../.gitbook/assets/image (409).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
// Setting the game server to the Lobby's owner
Lobby.SetGameServer();

// Let's set the game server to a specific ID
CSteamID fakeServerID =new();
Lobby.SetGameServer(fakeServerID);

// And now let's set a server by IP:Port
Lobby.SetGameServer("0.0.0.0", 7777);

// And finally, maybe we try hard and use all of it
Lobby.SetGameServer("0.0.0.0", 7777, fakeServerID);
```

We can then check the Game Server

```csharp
// You can read the current game server
if(Lobby.HasServer)
{
    LobbyGameServer server = Lobby.GameServer;

    CSteamID serverId = server.id;
    string ipAddress = server.IpAddress;
    ushort port = server.port;
}
```

You can and should also use the event system for example, you can listen when game server is set on any lobby you are a member of.

```csharp
// How to know when this was done?
SteamTools.Events.OnLobbyGameServer += HandleGameServerSet;
```

The handler for this would look like this

```csharp
private void HandleGameServerSet(LobbyData lobby, CSteamID server, string ip, ushort port)
{
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

The owner of the lobby can set Game Server information on the lobby when they are ready to notify members to connect to the server.

<figure><img src="../.gitbook/assets/image (344).png" alt=""><figcaption></figcaption></figure>

Doing this will cause an event to be raised on each member. You can bind this to the Steam Game Instance.

<figure><img src="../.gitbook/assets/image (345).png" alt=""><figcaption></figcaption></figure>

This indicates that it's time to connect to the server, and you can do that using the provided information, for example:

<figure><img src="../.gitbook/assets/image (348).png" alt=""><figcaption></figcaption></figure>

It is important to note that you can also check the Game Server info on a lobby, and in general, when you join a lobby, you should check.

<figure><img src="../.gitbook/assets/image (346).png" alt=""><figcaption></figcaption></figure>

And make sure that the server hasn't already been set, if it has you should likely connect to it, fior example.

<figure><img src="../.gitbook/assets/image (347).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}
## C\#

```csharp
CSteamID lobby; // The lobby to set it on

// You can set an IP it is optional, but if you do, Steam uses IP as an int
string ipString = 0.0.0.0; // We will need to convert this if we use IP
byte[] ipBytes = IPAddress.Parse(address).GetAddressBytes();
uint ip = (uint)ipBytes[0] << 24;
ip += (uint)ipBytes[1] << 16;
ip += (uint)ipBytes[2] << 8;
ip += (uint)ipBytes[3];

// Port is required if you use IP and not needed if you don't
ushort port; 7777;

// If it's a Steam Game Server, then it has an ID and can use it as an address
CSteamID gameServerId;

// Now set the address
SteamMatchmaking.SetLobbyGameServer(lobby, Utilities.IPStringToUint(ip), port, gameServerId);
```
{% endtab %}
{% endtabs %}

### Chat (Send/Receive)

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Lobby modular component to work with lobbies in your game.&#x20;

<figure><img src="../.gitbook/assets/image (414).png" alt=""><figcaption></figcaption></figure>

You can then add settings

<figure><img src="../.gitbook/assets/image (413).png" alt=""><figcaption></figcaption></figure>

The Chat UI settings help you set up a Chat UI for your lobby

### Max Messages

This is how many messages will be displayed in the scroll view at once. When the 201st message is received the 1st message will be destroyed.

### Chat Panel

This should be a parent object of the whole chat. The system will enable this when there is a lobby set, and disable it when not.

### Input Field

This will be monitored and when Enter or Return is pressed the chat message if any will be sent. You can optionally call the SendMessage() function such as from a button's Click event to cause the text to be sent.

### Scroll View

This will be managed so that it scrolls to the bottom as new messages are added.

### Message Root

This is where new messages will be spawned. You should apply a Vertical Layout control or similar

### My Chat Template

<figure><img src="../.gitbook/assets/image (415).png" alt=""><figcaption></figcaption></figure>

This will be spawned for each message the player sends. This should implement the Steam Lobby Member Chat Message component.

### Their Chat Template

<figure><img src="../.gitbook/assets/image (416).png" alt=""><figcaption></figcaption></figure>

This will be spawned for each message sent by lobby members other than the player. This should implement the Steam Lobby Member Chat Message component.

## C\#

```csharp
// First, you need to know the lobby to send this to
LobbyData Lobby = 123456798; // stand in for a real lobby ID

// Then you need to decide what to send
// This can be a string message
Lobby.SendChatMessage("Hello World");
// Or
// It can be a serializable structure or class
Lobby.SendChatMessage(SomeObjectIHave);

// In order to "listen" for chat messages, you should use
SteamTools.Events.OnLobbyChatMsg += HandleChatMessage;
```

The handler will take the form of

```csharp
private void HandleChatMessage(LobbyChatMsg ChatMsg)
{
    // ChatMsg.Message: The string message if you sent a string
    // ChatMsg.FromJson<YourDataType>(): Gets the object if that is what you sent
    // ChatMsg.sender: who sent the message
    // ChatMsg.lobby: what lobby was it sent to
    // ChatMsg.receivedTime: when you first saw the message
    // ChatMsg.type: the EChatEntryType of message, which should always be EChatEntryType.k_EChatEntryTypeChatMsg
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Steam Lobby is actually a chat room and it sends chat messages as serialized byte data meaning you can send complex objects if you care to serialize that to a byte\[].

<figure><img src="../.gitbook/assets/image (350).png" alt=""><figcaption></figcaption></figure>

When the user receives a message the Lobby Chat Msg event will be raised, our node will handle parsing to string for you in the event you sent a string otherwise you would need to deserialize the byte\[] your self.

<figure><img src="../.gitbook/assets/image (349).png" alt=""><figcaption></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}
## C\#

To send a string

```csharp
byte[] data; // we will store our data to send here
CSteamID lobby; // the lobby to send to

// Now let's send a string
data= System.Text.Encoding.UTF8.GetBytes("Hello World");
SteamMatchmaking.SendLobbyChatMsg(this, data, data.Length);
```

To send an object, first, we need an object

```csharp
[Serializable]
public struct SomeObjectWeCanSend
{
    public int intValue;
    public string stringValue;
    public bool youGetTheIdea;
}
```

Then we can do&#x20;

```csharp
byte[] data;

// We could send it as byte serialisation 
// but I find for debugging JSON is nier than Byte 
// and performance isn't a factor here so why not

SomeObjectWeCanSend jsonObject; // sets its data

// We could log this string so we can see the values easily
string jsonString = JsonUtility.ToJson(jsonObject); // get it as a string

// Now convert to bytes
data= System.Text.Encoding.UTF8.GetBytes(jsonString); // get its bytes

// now send it
SteamMatchmaking.SendLobbyChatMsg(this, data, data.Length);
```
{% endtab %}
{% endtabs %}
