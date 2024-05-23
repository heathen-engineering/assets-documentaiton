---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Game Server Browser Manager

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Meant to be added to your Server Browser UI this component simplifies the process of querying Steam Game Servers.

{% hint style="info" %}
Before you can browse game servers you need to have game servers.

Read [Steam Game Servers](../../../company/steam/steamworks/multiplayer/game-server-browser/) article before continuing
{% endhint %}

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class GameServerBrowserManager : MonoBehaviour
```

## Events

### evtSearchComplete

Invoked when a search request completes.

## Methods

### Get All Favorites

```csharp
public void GetAllFavorites();
```

Returns the list of favorite servers

### Get All Friends

```csharp
public void GetAllFriends();
```

Returns the list of friend servers

### Get All History

```csharp
public void GetAllHistory();
```

Returns the list of historical servers

### Get All Internet

```csharp
public void GetAllInternet();
```

Returns the list of internet (non-LAN) servers

### Get All LAN

```csharp
public void GetAllLan();
```

Returns the list of LAN servers

### Get All Spectator

```csharp
public void GetAllSpectator();
```

Returns the list of Spectator servers

### Get Server list

```csharp
public void GetServerList(type, callback);
```

```csharp
public void GetServerList(app, type, callback);
```

Returns a list of servers based on the type provided

### Ping Server

```csharp
public void PingServer(address, port, callback);
```

Fetches updated data for the target server

### Player Details

```csharp
public void PlayerDetails(entry, callback);
```

Clears the player list then requests fresh player data from Valve

### Server Rules

```csharp
public void ServerRules(entry, callback);
```

Clears the rules list then requests fresh rule data from Valve
