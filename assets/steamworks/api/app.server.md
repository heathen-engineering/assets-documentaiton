# App.Server

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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
