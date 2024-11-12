---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Game Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using HeathenEngineering.SteamworksIntegration;
```

```csharp
public struct GameData : IEquatable<AppId_t>, 
                        IEquatable<CGameID>, 
                        IEquatable<uint>, 
                        IEquatable<ulong>, 
                        IEquatable<AppData>, 
                        IComparable<AppData>, 
                        IComparable<AppId_t>, 
                        IComparable<uint>, 
                        IComparable<ulong>
```

A data wrapper around the Steam's concept of "game". This provides quick and efficient access to features and functions related to a Steam Game and lets you use GameData interchangeably with any of the related types `AppId_t, CGameID, uint, ulong`

```csharp
GameData game_fromUlong = 1234566;
GameData game_fromCGameID = new CGameID(1234566);
GameData game = GameData.Get(1234566);

GameData thisGame = GameData.Me;
```

Game Data is used by Steam to uniquely identify a "game". It can often be useful to convert the various forms in which Steam identifies a "game" such that you can get its name or open its store page.&#x20;

For example Steam identifies which game a user is the User's Game Info via CGameID which can be converted to an AppId\_t which can be used to get the uint and passed to the Web ID to get the name of the game the friend is playing.

Heathen makes this much simpler `GameData.Get(gameId).App.Name` as you can see our approach has far fewer steps thanks to GameData and AppData which provides the translation layer for the various ways Steam represents a Game and its related App ID.

## Fields and Attributes

### Me

```csharp
public static GameData Me => get;
```

This gets the GameData for the currently initialized app if any. I.e. this is your App ID represented as a GameData as in the one running right now as far as Steam API is aware. Its often useful to test this and make sure its the value you expect and that your user isn't trying to spoof as some other app.

### gameId

```csharp
public CGameID gameId;
```

The Steamworks native data type representation of this game

### App

```csharp
public AppData App;
```

Gets the AppData representation of this GameData. GameData and AppData are very similar with AppData being the more commonly used of the two. GameData is used in a few of Steam's systems such as GameInfo. Switching between them is made trivial with our data layer as a GameData will convert to an AppData and an AppData will convert to a GameData.

### IsMe

```csharp
public bool IsMe => get;
```

Returns true if this GameData represents the game that is running this code e.g. the same as

```csharp
thisAppId == GameData.Me
```

### Id

```csharp
public uint Id { get; set; }
```

The primitive data type that represents an app

### Name

```csharp
public string Name => get;
```

Gets the local display name Steam store uses for this game for this user ... this expects that you have already loaded the names via the LoadNames method here on the AppData object or in the API.App.Client class.

### Names Loaded

```csharp
public static bool NamesLoaded
```

Returns true if app names have already been loaded

## Methods

### Get

```csharp
//Returns the local app as a GameData
public static GameData Get();

//Returns the GameData matching the game ID
public static GameData Get(CGameID gameId)

//Returns the GameData matching the game ID
public static GameData Get(ulong gameId)

//Returns the GameData matching the app id
public static GameData Get(uint appId)

//Returns the GameData matching the app id
public static GameData Get(AppId_t appId)
```

The Get method can be used to "get" an GameData matching whatever input it is you have

### Get Name

```csharp
public bool GetName(out string name)
```

Returns true if the name is loaded and found and if so then name will be populated with the name, this is the same as reading the Name field.

```csharp
public void GetName(Action<string, bool> callback)
```

This is an async version that will check if the name is loaded, if not it will load it, when completed it will invoke the callback which takes the form of

```csharp
void Callback(string name, bool IOError)
{
    if(!IOError)
        Debug.Log($"The name is {name}");
}
```

### Open Steam Store

```csharp
public void OpenSteamStore(EOverlayToStoreFlag flag)
```

This is an instanced version of the method meaning you call it on a given AppData such as AppData.Me.OpenSteamStore();

Note that the input parameter named flag is optional and can be ignored, to see the available options please review [Valve's documentation on the subject](https://partner.steamgames.com/doc/api/ISteamFriends#EOverlayToStoreFlag).

```csharp
public static void OpenSteamStore(AppData app, EOverlayToStoreFlag flag)
```

A static option for calling the same method that can handle any convertable value for AppData for exmple

```csharp
uint appId = 123456789;
GameData.OpenSteamStore(appId);
```

Assuming 123456789 was a valid App ID that would open the steam overlay to the store page for that app

### Open My Steam Store

```csharp
public static void OpenMySteamStore(EOverlayToStoreFlag flag)
```

A static method to open the store for the current App
