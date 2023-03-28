# App Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public struct AppData : IEquatable<AppId_t>, 
                        IEquatable<CGameID>, 
                        IEquatable<uint>, 
                        IEquatable<ulong>, 
                        IEquatable<AppData>, 
                        IComparable<AppData>, 
                        IComparable<AppId_t>, 
                        IComparable<uint>, 
                        IComparable<ulong>
```

A data wrapper around the Steam's concept of "app". This provides quick and efficient access to features and functions related to a Steam App and lets you use AppData interchangeably with any of the related types `DlcData, AppId_t, CGameID, uint, ulong`

```csharp
AppData app_fromUlong = 1234566;
AppData app_fromCGameID = new CGameID(1234566);
AppData app = AppData.Get(1234566);

AppData thisApp = AppData.Me;
```

App Data is used by Steam to uniquely identify an "app" ... for Steam an "app" is a game, tool, server, dlc, demo or really anything similarly defined as part of the Steam Developer Portal. It can offten be useful to convert the various forms in which Steam idenitfies an "app" such that you can get its name or open its store page.&#x20;

For example Steam identifies which game a user is the User's Game Info via CGameID which can be converted to an AppId\_t which can be used to get the uint and passed to the Web ID to get the name of the game the friend is playing.

Heathen makes this much simpler `AppData.Get(gameId).Name` as you can see our approch has far fewer steps thanks to AppData which provides the translation layer for the various ways Steam represents an App's ID.

## Fields and Attributes

### Me

```csharp
public static AppData Me => get;
```

This gets the AppData for the currently initialized app if any. I.e. this is your App ID as in the one running right now as far as Steam API is aware. Its often useful to test this and make sure its the value you expect and that your user isn't trying to spoof as some other app.

### appId

```csharp
public AppId_t appId;
```

The Steamworks native data type representation of this app

### IsMe

```csharp
public bool IsMe => get;
```

Returns true if this AppData represents the app that is running this code e.g. the same as

```csharp
thisAppId == AppData.Me
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

Gets the local display name Steam store uses for this app for this user ... this expects that you have already loaded the names via the LoadNames method here on the AppData object or in the API.App.Client class.

### Names Loaded

```csharp
public static bool NamesLoaded
```

Returns true if app names have already been loaded

## Methods

### Get

```csharp
//Returns the local app
public static AppData Get();

//Returns the AppData matching the game ID
public static AppData Get(CGameID gameId)

//Returns the AppData matching the game ID
public static AppData Get(ulong gameId)

//Returns the AppData matching the app id
public static AppData Get(uint appId)

//Returns the AppData matching the app id
public static AppData Get(AppId_t appId)

//Returns the AppData matching the Dlc Data
public static AppData Get(DlcData dlcData);
```

The Get method can be used to "get" an AppData matching whatever input it is you have

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
AppData.OpenSteamStore(appId);
```

Assuming 123456789 was a valid App ID that would open the steam overlay to the store page for that app

### Open My Steam Store

```csharp
public static void OpenMySteamStore(EOverlayToStoreFlag flag)
```

A static method to open the store for the current App
