---
description: Discovering Steam Game Servers in Steam client or in game.
---

# 📋 Server Browser

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Steam Game Server Browser is a feature of the Steam client and Steam API that gives you a matchmaking and discovery tool for logged-on Steam Game Servers. In order to use this feature you will need to initialize your server build as a Steam Game Server and Log On to the server with Set Advertise Game Server as true.&#x20;

{% hint style="info" %}
Heathen's Steamworks Complete for Unity trivializes all of this, the [Steam Settings](../../../../../assets/steamworks/unity/scriptable-objects/steam-settings/) scriptable object contains all the configuration options so you can set them in the Unity inspector.&#x20;

Our initialization process is smart and will initialize for Steam Game Server for any server build and will use Steam Client for any client build. We do this by checking the standard unity script define `UNITY_SERVER`
{% endhint %}

## In Game Browser

The [Game Server Browser Manager](../../../../../assets/steamworks/unity/components/game-server-browser-manager.md) is a Unity component we designed to simplify the query of the Steam Game Server browser entries. Our browser manager works with the [Matchmaking.Client API](../../../../../assets/steamworks/api/matchmaking.md) to query Steam for lists of servers.

In general, servers are listed in the following groups and may appear in more than 1 group

* Favourites \
  Servers marked as favourite by the user who&#x20;
* Friends\
  Servers friends are associated with
* History\
  Servers the user has connected to in the past
* Internet\
  Servers that are not on the local area network e.g. internet servers
* LAN\
  Servers that are on the local area network
* Spectator\
  Spectator servers

Once you have a list of servers you can set up your own UI to display them and you can use our Browser Manger, our API or the raw Steam API to interrogate them e.g. request a refresh on Ping, Refresh the server rules and refresh Player Details.

## Raw API

The SteamMatchmakingServers API from Steam API is where you will find the Request\<type>ServerList, PingServer, PlayerDetails and related methods; for example&#x20;

```csharp
SteamMatchmakingServer.RequestInternetServerList(...);
```

Heathen's API contains this in `API.Matchmaking.Client` along with all other matchmaking-related features suitable for use in a client build.

