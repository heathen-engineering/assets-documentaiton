# Steam Settings

## Introduction

SteamSettings is the root of Heathen Engineering's Steamworks tools and systems. The SteamSettings provides access to all core functionalities including stats, achievements, the friends system and the overlay system.

{% hint style="info" %}
You can edit the existing Steam Settings included with the Demo Scenes or create your own Steam Settings in your Project tab by right clicking and selecting **Create > Steamworks > Settings**
{% endhint %}

SteamSettings inherits from ScriptableObject, which means it can be referenced at development time and across all scenes without the overhead a MonoBehavior brings with it.

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

### Fields and Attributes

{% hint style="info" %}
All static accessors can also be accessed by referene e.g.

```csharp
mySettings.applicationId
```

is the same as

```csharp
SteamSettings.ApplicationId
```
{% endhint %}

| Type                             | Name                      | Comment                                                        |
| -------------------------------- | ------------------------- | -------------------------------------------------------------- |
| SteamSettings                    | current                   | Static access to the currently initalized Seam Settings object |
| AppId\_t                         | ApplicationId             | Static access to the App ID                                    |
| bool                             | HasInitalizationError     | Static indicates some error on initalization                   |
| string                           | InitalizationErrorMessage | Static string for the current intialization error if any       |
| bool                             | Initialized               | Static indicates rather or not the API is initalzied           |
| GameClient                       | Client                    | Static access the client features                              |
| GameServer                       | Server                    | Static access to the server features                           |
| List\<AchievementObjects>        | Achievements              | Static access to the achievements list                         |
| List\<StatObject>                | Stats                     | Static access to the stat list                                 |
| List\<DownloadableContentObject> | DLC                       | Static access to the DLC list                                  |
| List\<LeaderboardObject>         | Leaderboards              | Static access to the Leaderboard list                          |
|                                  |                           |                                                                |

### Events

#### evtSteamInitalized

occurs when steam initalizes

#### evtSteamInitalizationError

occurs when steam initalization has an error

### Methods

```csharp
public void CreateBehaviour(bool doNotDestroy = false);
```

Used to create a SteamworksBehaviour at run time if required. If one is already present this will do nothing.

```csharp
public static void CreateBehaviour(SteamSettings settings,
                                   bool doNotDestoy = false);
```

Static version of CreteatBehaviiour
