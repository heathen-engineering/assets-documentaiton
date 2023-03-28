# DLC Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public struct DlcData : IEquatable<AppId_t>, 
                        IEquatable<uint>, 
                        IEquatable<AppData>, 
                        IComparable<AppData>, 
                        IComparable<AppId_t>, 
                        IComparable<uint>
```

Wraps the concept of a DLC in a simple struct. This struct is implicitly convertible to and from uint, AppData and the native Steam API type of AppId\_t

## Fields and Attributes

### AppId

```csharp
public AppId_t AppId => get;
```

Returns the native Steam API type AppId\_t for this DLC object

### Available

```csharp
public bool Available => get;
```

Returns true if the DLC is available to the user, false otherwise

### Name

```csharp
public bool Name => get;
```

Returns the localized name of the DLC for the user if any otherwise returns the default name

### Is Subscribed

```csharp
public bool IsSubscribed => get;
```

Returns true if the user is subscribed to this DLC ... that is does this user own or otherwise currently have access to this DLC.

### Is Installed

```csharp
public bool IsInstalled => get;
```

Returns true if the user has installed this DLC ...&#x20;

{% hint style="success" %}
note that most modern DLC do not have anything to install, typically in a modern game the "main" game contains all content and DLC ownership simply acts as an unlock. This is particularly important for multiplayer games where the content is required in order for players to play together.
{% endhint %}

### Install Directory

```csharp
public DirectoryInfo InstallDirectory => get;
```

The directory information if any, if the DLC is installed, this can be null.

### Download Progress

```csharp
public float DownloadProgress => get;
```

Returns a value from 0 to 1 indicating the download progress of the DLC if downloading is relivent.

### Earliest Purchase Time

```csharp
public DateTime EarliestPurchaseTime => get;
```

Note it may be possible for the user to have access to the DLC without having purchased, such as free weekened, barrowing from from friends and family, etc. If this date is older than the release of your game such as the 1st of January 1970 then the DLC has not been purchased.

## Methods

### Install

```csharp
public void Install()
```

Request the DLC be installed, this is a request and may be refused, Valve does not give feedback either way.

### Uninstall

```csharp
public void Uninstall()
```

Requests the DLC be uninstalled, this is a request and may be refused, Valve does not give feedback either way.

### Open Store

```csharp
public void OpenStore(EOverlayToStoreFlag flag = EOverlayToStoreFlag.k_EOverlayToStoreFlag_None)
```

Opens the Steam overlay to the DLC item's store page. The flag is optional, please see the [EOverlayToStoreFlag options here](https://partner.steamgames.com/doc/api/ISteamFriends#EOverlayToStoreFlag).

### Get

There are several static get methods that can be used to return a DlcData object based on various IDs

```csharp
public static DlcData Get(uint appId)
public static DlcData Get(AppId_t appId)
public static DlcData Get(AppData appData)
```

