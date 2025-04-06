# Getting Started

## Initialization

{% hint style="success" %}
1st and foremost ... if you have SteamManager.cs in your project remove it.

\
That script should not be used at all, it is not part of Heathen's Toolkit and it was not meant to be dragged and dropped into a production project in the first place.
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3>Code Free</h3></td><td><ul><li>Set your desired settings</li><li>Add component to game object </li><li>Done!</li></ul></td><td><a href="../../.gitbook/assets/image (4) (1) (1) (1).png">image (4) (1) (1) (1).png</a></td><td><a href="getting-started.md#component-1">#component-1</a></td></tr><tr><td><h3>With Configuraiton</h3></td><td><ul><li>Doesn't require a GameObject</li><li>Single line of code</li></ul></td><td><a href="../../.gitbook/assets/Screenshot 2023-01-30 111537.png">Screenshot 2023-01-30 111537.png</a></td><td><a href="getting-started.md#object-1">#object-1</a></td></tr><tr><td><h3>Pure Code</h3></td><td><ul><li>Doesn't require a GameObject</li><li>No ScriptableObject</li><li>Pure C#</li></ul></td><td><a href="../../.gitbook/assets/Screenshot 2023-01-30 111633.png">Screenshot 2023-01-30 111633.png</a></td><td><a href="getting-started.md#api-1">#api-1</a></td></tr></tbody></table>

## Pure Code

You do NOT require any GameObjects to make Steamworks run. You can simply call our App API extension to initialize as a Client or Server and our system will handle the rest for you including running callbacks and updating input when and where required.

### Namespace

```csharp
using Heathen.SteamworksIntegration.API;
```

### Client

Replace 480 with your own app ID

```csharp
App.Client.Initialize(480);
```

Optionally you can pass in additional data about your set-up, however, this is not usually done unless you are using Steam Settings objects in which case you can use them to initialize directly, see the Object section below.

### Server

```csharp
App.Client.Initialize(480, ServerConfig);
```

The server configuration is a structure where you can define the ports, and settings you want Steamworks to use with your Steam Game Server.

## Object

When you configured your Steam Settings it created `SteamSettings` objects that can be used to initialize directly. The Initialization function on these objects will read all required data from them and will select Client or Game Server based on the build type.

### Configure Settings

Open your Project Settings and select Player > Steamworks

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

When you first do this it will create a SteamMain Steam Settings object in your projects Settings folder.

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

You can optionally add a Demo setting and as many Playtest settings as you would like. All of them will be added to the Settings folder in their own Steam Settings object.

### Updating your Bootstrap

To do this, in a script that loads first in your game ideally where you're performing bootstrap and validation logic simply add a variable for Steam Settings, and then drag and drop the Steam Settings you would like to use.

Add a using statement

```csharp
using Heathen.SteamworksIntegration;
```

Add a variable of type Steam Settings

```csharp
[SerializeField]
private SteamSettings settings;
```

At an appropriate point in your bootstrap logic call Initialize

```csharp
settings.Initialize();
```

## Component

If you need a code-free solution we provide you with a component script `Initialize Steamworks` which will initialize the Steamworks SDK for you based on your configured Steam Settings.



<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

This component should be put on your first scene, you should make sure Steamworks has initiated before you make any use of it and ideally, before you load it into your main menu.

You DO NOT need to mark this component as Do Not Destroy on Load ... it does not need to persist between levels and only exists to call Initialize on the settings you chose.
