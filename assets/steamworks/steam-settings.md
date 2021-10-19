---
description: >-
  Steam settings are the root of the Steamworks integration from Heathen
  Engineering, from here you can access all other features.
---

# Steam Settings

## Introduction

SteamSettings is the root of Heathen Engineering's Steamworks tools and systems. The SteamSettings provides access to all core functionalities including stats, achievements, the friends system and the overlay system.

{% hint style="info" %}
You can edit the existing Steam Settings included with the Demo Scenes or create your own Steam Settings in your Project tab by right clicking and selecting **Create > Steamworks > Settings**
{% endhint %}

SteamSettings inherits from ScriptableObject, which means it can be referenced at development time and across all scenes without the overhead a MonoBehavior brings with it.

![Screen shot of the Example System Settings object located in the Steamworks Examples folder.](../../.gitbook/assets/image.png)

There are three ways to interact with and access the most important parts of SteamSettings at runtime.&#x20;

### SteamSettings.current

```csharp
public static SteamSettings current;
```

This is a static reference to the initialized SteamSettings object. It gets initialized when the Init Method gets called by the [Steamworks Behaviour](quick-start-guide/steamworks-behaviour.md) component.

### SteamSettings.Client

```csharp
public static GameClient Client => current.client;
```

This is a static reference to the initialized SteamSettings.GameClient. The GameClient member provides easy access to features and systems relevant for your "client", that is the application the end user is actually playing e.g. your game. This would include features such as overlay, friends, clans, stats, achievements, and more.

{% hint style="warning" %}
This and its related functionality is stripped out of the compile on server builds. That is this code will not compile and will not be available for use in headless / server builds.
{% endhint %}

### SteamSettings.Server

```csharp
public static GameServer Server => current.server;
```

This is a static reference to the initialized SteamSettings.GameServer. The GameServer member in contrast deals with the configuration of Steamworks server related features, and only comes into play for server builds.

{% hint style="warning" %}
This and its related functionality is stripped out of the compile on client builds. That is this code will not compile and will not be available for use in normal / client builds.
{% endhint %}

## Configuration

SteamSettings holds all the Steam API relevant configuration in form of ScriptableObjects. These can and will be accessed and used to interact with the Steam API.

### General

![Screen shot from the top of the Steam Settings object as it appears in the Unity Inspector](<../../.gitbook/assets/image (1).png>)

**Debugging**

Inside the Unity Editor you are able to enable and disable Steams verbose messages with a button located at the top of SteamSettings.

{% hint style="warning" %}
Debugging uses Unity's Debug.Log system, which is a slow process to execute. It should only be used for development builds.
{% endhint %}

**Conditional Compile**

Inside the Unity Editor you are able to enable and disable so called conditional compile with a button located at the top of SteamSettings.&#x20;

When enabled it creates a DEFINE inside Unity, which instructs the compiler to only compile relevant elements for the appropriate build target. For example, the SteamSettings.Server object will not be compiled on client builds and vice versa. In general, you should always have this enabled.

### Build Options

Inside the Unity Editor you are able to configure the Steam relevant build settings. Most important the Application ID of your Steam App. This one is a shared configuration between client and server.

![Screen shot of the SteamSettings inspector with the Client settings selected.](<../../.gitbook/assets/image (2).png>)

![Screen shot of the SteamSettings inspector with the Server settings selected.](<../../.gitbook/assets/image (3).png>)

#### Client

The Client section refers to settings applicable only to client builds. This includes the Notification Popup settings where you can indicate the anchor position and the offset from the anchor position in terms of pixels.

{% hint style="warning" %}
The notification popup is part of Steam Overlay, which does not work in the Unity Editor. To test the overlay and overlay features such as the popup position, please build and deploy your app so it can be ran from the Steam Client normally.
{% endhint %}

#### Server

The Server section refers to settings applicable only to server builds. This includes features, connection settings and general Steam Game Server configuration values.

{% hint style="info" %}
&#x20;Steam Game Server is a concept from Valve where in you register any server on Steam’s Steam Game Server backend such that users can browser for it via the Steam Game Server browser and use Steam’s Steam Game Server Matchmaking tools to find a server. You can read more about the feature here: [https://partner.steamgames.com/doc/features/multiplayer/game\_servers](https://partner.steamgames.com/doc/features/multiplayer/game\_servers)
{% endhint %}

The Server section contains the following options

* Auto Initialize \
  If enabled then the Steam Game Server API will initialize on start up
* Auto Logon \
  If enabled then after initialization the system will “logon” to the Steam Game Server back end, registering your server as a Steam Game Server
* Server Heartbeat \
  If enabled heartbeat will be sent to the Steam Game Server backend. This is required for proper use of the Steam Game Server Browser feature and is what updates the backend with your server state.
* Anonymous Server Login \
  This is typically enabled, most game servers’ logon to the Steam API via anonymous. It is possible however to disable this and use a token instead.
* Game Server Auth API \
  Should the server use Game Server Auth API for authentication. This is typically enabled.
* Password Protected \
  Should the server indicate that it requires a password. This simply causes the server entry on the Steam Game Server Browser to indicate that a password will be required by the server.
* Dedicated Server \
  Is the server a dedicated server. As with Password Protected this effect the information presented by the Steam Game Server Browser.
* Spectator Support \
  Enable if your server supports spectators
* Mirror Support \
  This is only available if you have Mirror installed. When enabled the system will attempt to call Start Server on Mirror’s NetworkManger after API initialization but before Logon insuring Mirror is up and ready before the server is listed on Steam Game Server backend.
* IP address \
  This is usually left as 0, it indicates the IP address the client should use to connect to the server.
* Ports : Game \
  This is the port the user should use to connect to the server
* Ports : Query \
  This is the port used by Steam’s systems to query the server information
* Ports : Spectator \
  This is the port used for spectator connections
* Server Name \
  Required field in order to register the server on Steam Game Server
* Description \
  This is usually the full name of your game
* Directory \
  The local path of your app e.g. “Spacewars” would be the value for app 480
* Map Name \
  The map used by the server
* Game Metadata \
  Additional data relevant to your game
* Max Player Count \
  Max number of players permitted
* Bot Player Count \
  Number of bot players

## Artifacts

Inside your Unity Editors Inspector, you are able to define your Steam relevant artifacts. These are ScriptableObjects and act as data containers for interaction between your game and Steam. These are created as children of the SteamSetings ScriptableObject.

{% hint style="info" %}
Note that you may need to click into another folder inside your project tab and return to the SteamSettings so the Unity Editor renders your changes.
{% endhint %}

![](<../../.gitbook/assets/image (4).png>)

![](<../../.gitbook/assets/image (5).png>)

### User Data

{% embed url="https://kb.heathenengineering.com/assets/steamworks/user-data" %}

### Stats Object

{% embed url="https://kb.heathenengineering.com/assets/steamworks/stats-object" %}

### Achievement Object

{% embed url="https://kb.heathenengineering.com/assets/steamworks/achievement-object" %}

### Leaderboard Object

{% embed url="https://kb.heathenengineering.com/assets/steamworks/leaderboard-object" %}

### Downloadable Content Object

{% embed url="https://kb.heathenengineering.com/assets/steamworks/downloadable-content-object" %}

### Data Models

{% embed url="https://kb.heathenengineering.com/assets/steamworks/data-models" %}
