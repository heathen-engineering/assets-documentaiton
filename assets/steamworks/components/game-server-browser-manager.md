# Game Server Browser Manager

## Introduction

Meant to be added to your Server Browser UI this component simplifies the process of querying Steam Game Servers

## Definition

### Events

#### evtSearchComplete

Invoked when a search request completes.

### Methods

```csharp
public void GetAllFavoritesEntry();
```

Returns the list of favorite servers

```csharp
public void GetAllFriends();
```

Returns the list of friend servers

```csharp
public void GetAllHistory();
```

Returns the list of historical servers

```csharp
public void GetAllInternet();
```

Returns the list of internet (non-LAN) servers

```csharp
public void GetAllLan();
```

Returns the list of LAN servers

```csharp
public void GetAllSpectator();
```

Returns the list of Spectator servers

```csharp
public void GetServerList(type, callback);
```

```csharp
public void GetServerList(app, type, callback);
```

Returns a list of servers based on the type provided

```csharp
public void PingServer(address, port, callback);
```

Fetches updated data for the target server

```csharp
public void PlayerDetails(entry, callback);
```

Clears the player list then requests fresh player data from Valve

```csharp
public void ServerRules(entry, callback);
```

Clears the rules list then requests fresh rule data from Valve
