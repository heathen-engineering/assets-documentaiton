---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# App.Server

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Provides for initialization and registration of a Steam Game Server configuraiton.

## Fields and Attributes

### ID

Returns the ID issued to the Steam Game Server on initalization.

```csharp
public static CSteamID ID => get;
```

### LoggedOn

Indicates rather or not the server is logged on

```csharp
public static bool LoggedOn => get;
```

### Configuration

Defines the configuration of the server, this will be set by the Initialize method

```csharp
public static SteamGameServerConfiguraiton Configuraiton => get;
```

### Initialized

This is a global field located on API.App.Initialized and indicates rather or not the system is initialized.

{% hint style="info" %}
This is \***Not**\* located in the API.App.Server class rather its in the parent API.App class so to access it&#x20;

```csharp
if(API.App.Initalized)
    ;//Yes it is initalized
else
    ;//No it is not
```
{% endhint %}

```csharp
public static bool API.App.Initalized => get;
```

## Methods

### Initialize

Initializes the Steam API for client processing. If your using [SteamSettings](../quick-start-guide/scriptableobject-initialization.md) or [SteamworksBehaviour](../quick-start-guide/gameobject-initialization.md) this is done for you. You should only call this if you are not using [SteamSettings.Initialize](../scriptable-objects/steam-settings/#initialize) or the [SteamworksBehaviour](../components/steamworks-behaviour.md).

If used you will need to provide a [Steam Game Server Configuration](../objects/steam-game-server-configuration.md), this can be write and read from a JSON formatted file or set up as a structure and passed in.

```csharp
public static Initialize(AppData appId, SteamGameServerConfiguration config);
```

### LogOn

Logs the initialized server API on to the steam backend. If your Steam Game Server Settings is configured for auto logon this will be called for you once the API is initialized.

```csharp
public static void LogOn()
```

### Send Updated Server Details To Steam

Updates the server details based on the active configuration. This is called for you when the server first connects.

```csharp
public static void SendUpdatedServerDetailsToSteam()
```
