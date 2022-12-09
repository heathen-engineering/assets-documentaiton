# App.Server

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

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

Defines the configuration of the server, this will be set by the Initalize method

```csharp
public static SteamGameServerConfiguraiton Configuraiton => get;
```

### Initialized

This is a global field located on API.App.Initalized and indicates rather or not the system is initialized.

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

Initializes the the Steam API for client processing. If your using SteamSettings or SteamworksBehaviour this is done for you. You should only call this if you are not using SteamSettings.Initialize or SteamworksBehaviour.

```csharp
public static Initialize(AppData appId, SteamGameServerConfiguration config);
```
