# Matchmaking

## Introduction

```csharp
public static class API.Matchmaking
```

The whole of the matchmaking system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.Matchmaking.Client
```

### What can it do?

The matchmaking system is fundamentally a system for getting player's together in order to play games. The main feature of the sytem is the Steam Lobby. Steam Lobbies can be searched for based on the metadata of a lobby, they can be advertised via Party Beacons, on the friends list and direct invites can be sent to targeted players.

Steam Lobby can be used for more than a simple game lobby, depending on your games specific needs they can provide for teams, party/groups, session merging and more. Valve allows a user to be a member of 1 "normal" lobby and up to 2 additional "invisible" lobbies. Each lobby has its own set of metadata for the lobby its self and for each of its members and each lobby includes a simple chat system.

{% hint style="info" %}
Take a look at the Lobby Manager for a tool that can help you manage a specifc uses for a Steam Lobby and which can simplify lobby interactions and facilitate lobby UIs.
{% endhint %}

### Related Componenets

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

### Lobby Enter

Recieved upon attempting to enter a lobby. Lobby metadata is available to use immediately after receiving this.

### Lobby Data Update

The lobby metadata has changed.

### Lobby Chat Msg

A chat (text or binary) message for this lobby has been received.

### Favorites List Changed

A server was added/removed from the favorites list, you should refresh now.

### Lobby Chat Update

A lobby chat room state has changed, this is usually sent when a user has joined or left the lobby.

### Lobby Game Created

A game server has been set via [Set Lobby Game Server](matchmaking.md#undefined) for all of the members of the lobby to join. It's up to the individual clients to take action on this; the typical game behavior is to leave the lobby and connect to the specified game server; but the lobby may stay open throughout the session if desired.

### Lobby Invite

Someone has invited you to join a Lobby. Normally you don't need to do anything with this, as the Steam UI will also display a '\<user> has invited you to the lobby, join?' notification and message.\
\
If the user outside a game chooses to join, your game will be launched with the parameter `+connect_lobby <64-bit lobby id>`

### Lobby Leave

Invoked when API.Matchmaking.Client.LeaveLobby is called

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
