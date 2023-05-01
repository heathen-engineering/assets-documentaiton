---
description: Configuration and easy access to key artefacts
---

# Steam Settings

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

SteamSettings is the root of Heathen's Steamworks.

{% hint style="info" %}
You can edit the existing Steam Settings included with the Demo Scenes or create your own Steam Settings in your Project tab by right clicking and selecting **Create > Steamworks > Settings**
{% endhint %}

SteamSettings inherits from ScriptableObject, which means it can be referenced at development time and across all scenes without the overhead a MonoBehavior brings with it. In addition the SteamSettings object includes static references to the active Steamworks Behaviour, Client settings DLC, Stats and Achievements and most other referenced artefacts.

There are three ways to interact with and access the most important parts of SteamSettings at runtime.&#x20;

### SteamSettings.current

```csharp
public static SteamSettings current;
```

This is a static reference to the initialized SteamSettings object. It gets initialized when the Init Method gets called by the [Steamworks Behaviour](broken-reference) component.

### SteamSettings.Client

```csharp
public static GameClient Client => current.client;
```

This is a static reference to the initialized SteamSettings.GameClient. The GameClient member provides easy access to features and systems relevant for your "client", that is the application the end user is actually playing e.g. your game. This would include features such as overlay, friends, clans, stats, achievements, and more.

### SteamSettings.Server

```csharp
public static GameServer Server => current.server;
```

This is a static reference to the initialized SteamSettings.GameServer. The GameServer member in contrast deals with the configuration of Steamworks server related features, and only comes into play for server builds.

{% hint style="warning" %}
This and its related functionality is stripped out of the compile on client builds. That is this code will not compile and will not be available for use in normal / client builds.
{% endhint %}

## Definition

```csharp
public class SteamSettings : ScriptableObject
```

## Fields and Attributes

### Current

```csharp
public static SteamSettings current;
```

A static reference to the currently initialized Steam Settings object.

### Behaviour

```csharp
public static SteamworksBehaviour behaviour;
```

A static reference to the Steamworks Behaviour that initialized the Steam API and is managing the Steam update loop.

### Leaderboards

```csharp
public static List<LeaderboardObject> Leaderboards => get;
```

A static reference to the collection of [leaderboard objects](../leaderboard-object.md) being managed by the system.

### DLC

```csharp
public static List<DownloadableContentObject> DLC => get;
```

A static reference to the collection of [downloadable content objects](../downloadable-content-object.md) being managed by the system.

### Stats

```csharp
public static List<StatObject> Stats => get;
```

A static reference to the collection of stat objects being managed by the system. This includes both [Int ](../int-stat.md)and [Float](../float-stat.md) based stats.

### Achievements

```csharp
public static List<AchievementObject> Achievements => get;
```

A static reference to the collection of achievement objects being managed by the system.

### Application Id

```csharp
public static AppId_t ApplicationId => get;
```

A static reference to the App ID recorded for the active settings object.

### Has Initialization Error

```csharp
public static bool HasInitalizationError => get;
```

A static valid indicating rather or not the API experienced an error on initialization.

### Initialization Error Message

```csharp
public static string InitalizationErrorMessage => get;
```

If initialization had an error a message will be available in this field indicating what or why.

### Initialized

```csharp
public static bool Initialized => get;
```

A static value indicating rather or not the Steam API has been initialized.

### Client

```csharp
public static GameClient Client => get;
```

A static reference to the active client tools and features if available. Note it is possible to have this stripped out of compilation for server builds.

### Server

```csharp
public static GameServer Server => get;
```

A static reference to the active server tools and features if available. Note it is possible to have this stripped out of compilation for client builds.

## Events

### evtSteamInitalized

occurs when steam initializes, This event handler does not take any arguments

```csharp
private void HandleSteamInitialized()
{
    if(StemSettings.Initialized)
        ;//Yep
    else
        ;//Should never happen but no not working
}
```

### evtSteamInitalizationError

occurs when steam initialization has an error, This event handler provides a string message indicating the likely problem or response from Steam.

```csharp
private void HandleSteamInitializeationError(string errorMessage)
{
    //Steam API cannot initalize and the message says why
}
```

## Methods

### Init

```csharp
public void Init()
```

Initializes the Steam API based on the configuration settings defined in the settings object.

### Create Behaviour

```csharp
public void CreateBehaviour(bool doNotDestroy = false);
```

Used to create a SteamworksBehaviour at run time if required. If one is already present this will do nothing.

```csharp
public static void CreateBehaviour(SteamSettings settings,
                                   bool doNotDestoy = false);
```

Static version of CreteatBehaviiour
