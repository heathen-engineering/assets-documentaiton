# Matchmaking

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

```csharp
using API = HeathenEngineering.SteamworksIntegraiton.API;
```

```csharp
public static class API.Matchmaking
```

The whole of the matchmaking system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Matchmaking.Client
```

{% hint style="info" %}
TIP

\
Save your self some typing. add this using statement to the top of any script that will need to use this API.

```csharp
using Matchmaking = HeathenEngineering.Steamworks.API.Matchmaking.Client;
```

\
You can now access members in this API with a shorter call structure

```csharp
var data = Matchmaking.GetLobbydata(lobby);
```



as opposed to the long form:

```csharp
var data = API.Matchmaking.Client.GetLobbydata(lobby);
```
{% endhint %}

### What can it do?

The matchmaking system is fundamentally a system for getting player's together in order to play games. The main feature of the sytem is the Steam Lobby. Steam Lobbies can be searched for based on the metadata of a lobby, they can be advertised via Party Beacons, on the friends list and direct invites can be sent to targeted players.

Steam Lobby can be used for more than a simple game lobby, depending on your games specific needs they can provide for teams, party/groups, session merging and more. Valve allows a user to be a member of 1 "normal" lobby and up to 2 additional "invisible" lobbies. Each lobby has its own set of metadata for the lobby its self and for each of its members and each lobby includes a simple chat system.

{% hint style="info" %}
Take a look at the Lobby Manager for a tool that can help you manage a specifc uses for a Steam Lobby and which can simplify lobby interactions and facilitate lobby UIs.
{% endhint %}

### Related Componenets

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/game-server-browser-manager" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/lobby-manager" %}
Simplify Steam Lobbies
{% endembed %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/lobby-chat-director" %}
Connect your UI to lobby chat quickly and easily
{% endembed %}

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/lobby" %}
Represents a lobby and  simplifies accessing it members, data, chat and more
{% endembed %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/lobby-chat-msg" %}
Lobby chat messages made easy
{% endembed %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/lobby-game-server" %}
How you know where to go
{% endembed %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/lobby-member" %}
Represents a lobby member and simplies accessing its data
{% endembed %}

## Events

### EventLobbyEnterSuccess

Occurs when a lobby enter callback is recieved and the responce code is a success

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LobbyEnter_t result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyEnterSuccess.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyEnterSuccess.RemoveListener(HandleEvent);
}
```

### EventLobbyEnterFailed

Occurs when a lobby enter callback is received and the responce code is not a success.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LobbyEnter_t result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyEnterFailed.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyEnterFailed.RemoveListener(HandleEvent);
}
```

### EventLobbyDataUpdate

Occurs when the lobby metadata has changed.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LobbyDataUpdate_t result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyDataUpdate.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyDataUpdate.RemoveListener(HandleEvent);
}
```

### EventLobbyChatMsg

Occurs when a chat (text or binary) message for this lobby has been received. After getting this you must use GetLobbyChatEntry to retrieve the contents of this message.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LobbyChatMsg result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.LobbyChatMsgEvent.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.LobbyChatMsgEvent.RemoveListener(HandleEvent);
}
```

### EventFavoritesListChanged

A server was added/removed from the favorites list, you should refresh now.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(FavoritesListChanged_t result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventFavoritesListChanged.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventFavoritesListChanged.RemoveListener(HandleEvent);
}
```

### EventLobbyChatUpdate

A lobby chat room state has changed, this is usually sent when a user has joined or left the lobby.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LobbyChatUpdate_t result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyChatUpdate.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyChatUpdate.RemoveListener(HandleEvent);
}
```

### EventLobbyGameCreated

A game server has been set via [Set Lobby Game Server](matchmaking.md#undefined) for all of the members of the lobby to join. It's up to the individual clients to take action on this; the typical game behavior is to leave the lobby and connect to the specified game server; but the lobby may stay open throughout the session if desired.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LobbyGameCreated_t result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyGameCreated.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyGameCreated.RemoveListener(HandleEvent);
}
```

### EventLobbyInvite

Someone has invited you to join a Lobby. Normally you don't need to do anything with this, as the Steam UI will also display a '\<user> has invited you to the lobby, join?' notification and message.\
\
If the user outside a game chooses to join, your game will be launched with the parameter `+connect_lobby <64-bit lobby id>`

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(LobbyInvite_t result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyInvite.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyInvite.RemoveListener(HandleEvent);
}
```

### EventLobbyLeave

Invoked when API.Matchmaking.Client.LeaveLobby is called

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(Lobby result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyLeave.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyLeave.RemoveListener(HandleEvent);
}
```

### EventLobbyAskedToLeave

The local user has been asked to leave a lobby. In general you should handle this event and leave when asked assuming your game has implamented kick lobby.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(Lobby result)
{
}
```

Then you would register the event such as:

```csharp
API.Matchmaking.Client.EventLobbyAskedToLeave.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    API.Matchmaking.Client.EventLobbyAskedToLeave.RemoveListener(HandleEvent);
}
```

## Fields and Attributes

### MemberOfLobbies

This list is populated by the system as the user creates, joins and leaves lobbies. It is a list of lobbies the user is currently a member of.

```csharp
public static List<Lobby> memberOfLobbies => get;
```

You can call this field via

```csharp
foreach(var lobby in API.Matchmaking.Client.memberOfLobbies)
{
    Debug.Log("Member of lobby: " + lobby.Name);
}
```

## Methods

### AddHistoryGame

Adds the game server to the local favorites list or updates the time played of the server if it already exists in the list.

```csharp
public static void AddHistoryGame(AppId_t appID, 
                uint ipAddress, 
                ushort port, 
                ushort queryPort, 
                DateTime lastPlayedOnServer)
```

### AddFavoriteGame

Adds the game server to the local favorites list or updates the time played of the server if it already exists in the list.

```csharp
public static void AddFavoriteGame(AppId_t appID, 
                uint ipAddress, 
                ushort port, 
                ushort queryPort, 
                DateTime lastPlayedOnServer)
```

### AddHistoryGame

Adds the game server to the local favorites list or updates the time played of the server if it already exists in the list.

```csharp
public static void AddHistoryGame(AppId_t appID, 
                string ipAddress, 
                ushort port, 
                ushort queryPort, 
                DateTime lastPlayedOnServer)
```

### AddFavoriteGame

Adds the game server to the local favorites list or updates the time played of the server if it already exists in the list.

```csharp
public static void AddFavoriteGame(AppId_t appID, 
                string ipAddress, 
                ushort port, 
                ushort queryPort, 
                DateTime lastPlayedOnServer)
```

### AddRequestLobbyListDistanceFilter

Sets the physical distance for which we should search for lobbies, this is based on the users IP address and a IP location map on the Steam backed.

```csharp
public static void AddRequestLobbyListDistanceFilter(ELobbyDistanceFilter distanceFilter)
```

### AddRequestLobbyListFilterSlotsAvailable

Filters to only return lobbies with the specified number of open slots available.

```csharp
public static void AddRequestLobbyListFilterSlotsAvailable(int slotsAvailable)
```

### AddRequestLobbyListNearValueFilter

Sorts the results closest to the specified value.

Near filters don't actually filter out values, they just influence how the results are sorted. You can specify multiple near filters, with the first near filter influencing the most, and the last near filter influencing the least.

```csharp
public static void AddRequestLobbyListNearValueFilter(string key, int value)
```

### AddRequestLobbyListNumericalFilter

Adds a numerical comparison filter to the next RequestLobbyList call.

```csharp
public static void AddRequestLobbyListNumericalFilter(string key, 
                                int value, 
                                ELobbyComparison comparison)
```

### AddRequestLobbyListResultCountFilter

Sets the maximum number of lobbies to return. The lower the count the faster it is to download the lobby results & details to the client.

```csharp
public static void AddRequestLobbyListResultCountFilter(int max)
```

### AddRequestLobbyListStringFilter

Adds a string comparison filter to the next RequestLobbyList call.

```csharp
public static void AddRequestLobbyListStringFilter(string key, 
                                string value, 
                                ELobbyComparison comparison)
```

### CreateLobby

Create a new matchmaking lobby.

```csharp
public static void CreateLobby(ELobbyType type, 
                int maxMembers, 
                Action<Lobby, bool> callback)
```

### DeleteLobbyData

Removes a metadata key from the lobby.

```csharp
public static bool DeleteLobbyData(Lobby lobby, string key)
```

### GetFavoriteGame

Gets the details of the favorite game server by index.

```csharp
public static FavoriteGame? GetFavoriteGame(int index)
```

### GetFavoriteGames

Returns the collection of favorite game entries

```csharp
public static FavoriteGame[] GetFavoriteGames()
```

### GetFavoriteGameCount

Gets the number of favorite and recent game servers the user has stored locally.

```csharp
public static int GetFavoriteGameCount()
```

### GetLobbyData

Gets the metadata associated with the specified key from the specified lobby.

```csharp
public static string GetLobbyData(Lobby lobby, string key)
```

```csharp
public static Dictionary<string, string> GetLobbyData(Lobby lobby)
```

### GetLobbyGameServer

Gets the details of a game server set in a lobby.

```csharp
public static LobbyGameServer GetLobbyGameServer(Lobby lobby)
```

### GetLobbyMembers

Returns a list of user IDs for the members of the indicated lobby

{% hint style="warning" %}
The current user must be in the lobby to retrieve the Steam IDs of other users in that lobby.
{% endhint %}

```csharp
public static LobbyMember[] GetLobbyMembers(Lobby lobby)
```

### GetLobbyMemberLimit

The current limit on the # of users who can join the lobby.

```csharp
public static int GetLobbyMemberLimit(Lobby lobby)
```

### GetLobbyOwner

Returns the current lobby owner.

```csharp
public static CSteamID GetLobbyOwner(Lobby lobby)
```

### InviteUserToLobby

Invite another user to the lobby.

```csharp
public static bool InviteUserToLobby(Lobby lobby, UserData user)
```

### JoinLobby

Joins an existing lobby.

```csharp
public static void JoinLobby(Lobby lobby, Action<LobbyEnter_t, bool> callback)
```

### LeaveLobby

Leave a lobby that the user is currently in; this will take effect immediately on the client side, other users in the lobby will be notified by a LobbyChatUpdate\_t callback.

```csharp
public static void LeaveLobby(Lobby lobby)
```

### RemoveFavoriteGame

Removes the game server from the local favorites list.

```csharp
public static bool RemoveFavoriteGame(AppId_t appId, 
                uint ip, 
                ushort connectionPort, 
                ushort queryPort)
```

### RemoveHistoryGame

Removes the game server from the local history list.

```csharp
public static bool RemoveHistoryGame(AppId_t appId, 
                uint ip, 
                ushort connectionPort, 
                ushort queryPort)
```

### RequestLobbyData

Refreshes all of the metadata for a lobby that you're not in right now.

{% hint style="info" %}
If your in the lobby then its data is always up to date
{% endhint %}

```csharp
public static bool RequestLobbyData(Lobby lobby)
```

### RequestLobbyList

Get a filtered list of relevant lobbies.

There can only be one active lobby search at a time. The old request will be canceled if a new one is started. Depending on the users connection to the Steam back-end, this call can take from 300ms to 5 seconds to complete, and has a timeout of 20 seconds.

{% hint style="info" %}
To filter the results you MUST call the AddRequestLobbyList\* functions before calling this. The filters are cleared on each call to this function.
{% endhint %}

{% hint style="info" %}
If AddRequestLobbyListDistanceFilter is not called, k\_ELobbyDistanceFilterDefault will be used, which will only find matches in the same or nearby regions.
{% endhint %}

{% hint style="info" %}
This will only return lobbies that are not full, and only lobbies that are k\_ELobbyTypePublic or k\_ELobbyTypeInvisible, and are set to joinable with SetLobbyJoinable.
{% endhint %}

```csharp
public static void RequestLobbyList(Action<Lobby[], bool> callback)
```

### SendLobbyChatMsg

Broadcasts a chat (text or binary data) message to the all of the users in the lobby.

```csharp
public static bool SendLobbyChatMsg(Lobby lobby, byte[] messageBody)
```

### SetLobbyData

Sets a key/value pair in the lobby metadata. This can be used to set the the lobby name, current map, game mode, etc.

{% hint style="info" %}
This can only be set by the owner of the lobby. Lobby members should use SetLobbyMemberData instead.
{% endhint %}

```csharp
public static bool SetLobbyData(Lobby lobby, string key, string value)
```

### SetLobbyGameServer

Sets the game server associated with the lobby.

{% hint style="info" %}
This can only be set by the owner of the lobby.
{% endhint %}

Either the IP/Port or the Steam ID of the game server must be valid, depending on how you want the clients to be able to connect.

A LobbyGameCreated\_t callback will be sent to all players in the lobby, usually at this point, the users will join the specified game server.

```csharp
public static void SetLobbyGameServer(Lobby lobby, 
                uint ip, 
                ushort port, 
                CSteamID gameServerId)
```

### SetLobbyJoinable

Sets whether or not a lobby is joinable by other players. This always defaults to enabled for a new lobby.

If joining is disabled, then no players can join, even if they are a friend or have been invited.

```csharp
public static bool SetLobbyJoinable(Lobby lobby, bool joinable)
```

### GetLobbyMemberData

Gets per-user metadata from another player in the specified lobby.

```csharp
public static string GetLobbyMemberData(Lobby lobby, CSteamID member, string key)
```

### GetMember

Get the LobbyMember object for a given user

```csharp
public static bool GetMember(Lobby lobby, CSteamID id, out LobbyMember member)
```

### IsAMember

Checks if a user is a member of this lobby

```csharp
public static bool IsAMember(Lobby lobby, CSteamID id)
```

### SetLobbyMemberData

Sets per-user metadata for the local user.

Each user in the lobby will be receive notification of the lobby data change via a LobbyDataUpdate\_t callback, and any new users joining will receive any existing data.

```csharp
public static void SetLobbyMemberData(Lobby lobby, string key, string value)
```

### SetLobbyMemberLimit

Set the maximum number of players that can join the lobby.

```csharp
public static bool SetLobbyMemberLimit(Lobby lobby, int maxMembers)
```

### SetLobbyOwner

Changes who the lobby owner is.

This can only be set by the owner of the lobby. This will trigger a LobbyDataUpdate\_t for all of the users in the lobby, each user should update their local state to reflect the new owner. This is typically accomplished by displaying a crown icon next to the owners name.

```csharp
public static bool SetLobbyOwner(Lobby lobby, CSteamID newOwner)
```

### SetLobbyType

Updates what type of lobby this is.

```csharp
public static bool SetLobbyType(Lobby lobby, ELobbyType type)
```

### CancelQuery

Cancel an outstanding server list request.

```csharp
public static void CancelQuery(HServerListRequest request)
```

### CancelServerQuery

Cancel an outstanding individual server query.

```csharp
public static void CancelServerQuery(HServerQuery query)
```

### GetServerCount

Gets the number of servers in the given list.

```csharp
public static int GetServerCount(HServerListRequest request)
```

### GetServerDetails

Get the details of a given server in the list. or get all servers as an array

```csharp
public static gameserveritem_t GetServerDetails(
        HServerListRequest request, 
        int index)
```

```csharp
public static gameserveritem_t[] GetServerDetails(
        HServerListRequest request)
```

### IsRefreshing

Checks if the server list request is currently refreshing.

```csharp
public static bool IsRefreshing(HServerListRequest request)
```

### PingServer

Queries an individual game servers directly via IP/Port to request an updated ping time and other details from the server.

```csharp
public static HServerQuery PingServer(uint ip, 
                ushort port, 
                ISteamMatchmakingPingResponse responce)
```

### PlayerDetails

Queries an individual game servers directly via IP/Port to request the list of players currently playing on the server.

```csharp
public static HServerQuery PlayerDetails(uint ip, 
                ushort port, 
                ISteamMatchmakingPlayersResponse responce)
```

### RefreshQuery

Ping every server in your list again but don't update the list of servers.

```csharp
public static void RefreshQuery(HServerListRequest request)
```

### RefreshServer

Refreshes a single server inside of a query.

```csharp
public static void RefreshServer(HServerListRequest request, int index)
```

### ReleaseRequest

Releases the asynchronous server list request object and cancels any pending query on it if there's a pending query in progress.

```csharp
public static void ReleaseRequest(HServerListRequest request)
```

### RequestFavoritesServerList

Request a new list of game servers from the 'favorites' server list.

```csharp
public static HServerListRequest RequestFavoritesServerList(AppId_t appId, 
                MatchMakingKeyValuePair_t[] filters, 
                ISteamMatchmakingServerListResponse pRequestServersResponse)
```

### RequestFriendsServerList

Request a new list of game servers from the 'friends' server list.

```csharp
public static HServerListRequest RequestFriendsServerList(AppId_t appId, 
                MatchMakingKeyValuePair_t[] filters, 
                ISteamMatchmakingServerListResponse pRequestServersResponse)
```

### RequestHistoryServerList

Request a new list of game servers from the 'history' server list.

```csharp
public static HServerListRequest RequestHistoryServerList(AppId_t appId, 
                MatchMakingKeyValuePair_t[] filters, 
                ISteamMatchmakingServerListResponse pRequestServersResponse)
```

### RequestInternetServerList

Request a new list of game servers from the 'internet' server list.

```csharp
public static HServerListRequest RequestInternetServerList(AppId_t appId, 
                MatchMakingKeyValuePair_t[] filters, 
                ISteamMatchmakingServerListResponse pRequestServersResponse)
```

### RequestLANServerList

Request a new list of game servers from the 'LAN' server list.

```csharp
public static HServerListRequest RequestLANServerList(AppId_t appId,  
                ISteamMatchmakingServerListResponse pRequestServersResponse)
```

### RequestSpectatorServerList

Request a new list of game servers from the 'favorites' server list.

```csharp
public static HServerListRequest RequestSpectatorServerList(AppId_t appId, 
                MatchMakingKeyValuePair_t[] filters, 
                ISteamMatchmakingServerListResponse pRequestServersResponse)
```

### ServerRules

Queries an individual game servers directly via IP/Port to request the list of rules that the server is running. (See ISteamGameServer::SetKeyValue to set the rules on the server side.)

```csharp
public static HServerQuery ServerRules(uint ip, 
                ushort port, 
                ISteamMatchmakingRulesResponse responce)
```

### LeaveAllLobbies

Leaves all lobbies the user is a member of if any

```csharp
public static void LeaveAllLobbies()
```

## How To

### Join Lobby

To join a lobby you need to know that lobby's ID and can simply call

```csharp
API.Matchmaking.Client.JoinLobby(id, callback);
```

### Create Lobby

Crete a new matcmaking lobby

```csharp
API.Matchmaking.Client.CreateLobby(type, maxMembers, callback);
```

This will create a new lobby of the type indicated, the local user will be automatically joined to the lobby and the callback will contains the Lobby reference of the lobby created in the result.

### Find a lobby

The Lobby Manager tool can help you create a lobby UI and simplify the various interactions with the lobby system. Alternativly you can search for a lobby manually.

To search manually you will call the various "Add Request" methods to build up your search paramiters those include

* Add Request Lobby List DIstance Filter
* Add Request Lobby List Filter Slots Available
* Add Request Lobby List Near Value Filter
* Add Request lobby List Numerical Filter
* Add Request Lobby list result Count Filter
* Add Request Lobby List String Filter

When you have built up the desired search paramiters you will need to call&#x20;

```csharp
API.Matchmaking.Client.RequestLobbyList(callback);
```

The callback will contain an array of the lobbies found.

{% hint style="warning" %}
The query paramiters are cleared on each call to Request Lobby List

There is no way to remove paramiters other than to request the lobby list and then start again from scratch.
{% endhint %}

{% hint style="info" %}
This will return a priority sorted list of lobbies which are of type Public or Invisible and are set to Joinable.
{% endhint %}

### Invite user to lobby

TO invite a user to a lobby you only need to know which lobby you and which user you wish to perform the operation on

```csharp
API.Matchmaking.Client.InviteUserToLobby(lobby, user);
```

### Set Lobby Game Server

This sets the game server assoceated with the lobby. When its first set it will raise the Lobby Game Server set event for all members. That event will contain conneciton information or user's can read the conneciton information from the lobby via the `GetLobbyGameServer` feature.

```csharp
API.Matchmaking.Client.SetLobbyGameServer(lobby, ip, port, serverId);
```
