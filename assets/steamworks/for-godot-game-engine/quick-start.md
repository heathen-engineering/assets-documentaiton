# Quick Start

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

{% hint style="info" %}
Steamworks.NET is dependent on ... .NET\
Our scripts are all C# based\
\
Consequently you should be using Godot (mono) or a similarly .NET compatible version of Godot.
{% endhint %}

Your first stop for getting started as a Steam Developer should be our [Guides on Steam](../../../company/steam/) its self including its [Quick Start](../../../company/steam/quick-start.md#introduction) guide. While you can perform very basic functional testing using the "Test App" 480 you really will need to secure your own App ID before you can do anything meaningful with Steam.

## Auto Load

When you activated the plugin it should have added a Steamworks Behaviour Auto Load entry

<figure><img src="../../../.gitbook/assets/image (192).png" alt=""><figcaption></figcaption></figure>

If that is missing simply add and enable it, it is the script

`addons/Heathen/SteamworksBehaviour.cs`

This should be the highest entry in the list of Auto Load scripts

## Your App ID

Once you have your own App ID you will need to update your project configuration to use it.

### Steamworks Behaviour

#### Step 1

Open `addons/Heathen/SteamworksBehaviour.cs` in Visual Studio or a similar scripting environment.

#### Step 2

Locate the `_Ready()` method on line 20 of the script and within it find the line shown below

```csharp
/*********************************************************
* Update this with your App ID
* Dont forget to also update the steam_appid.txt file
********************************************************/
AppId_t applicationId = new AppId_t(480);
```

#### Step 3

Replace `480` with your App ID number

```csharp
/*********************************************************
* Update this with your App ID
* Dont forget to also update the steam_appid.txt file
********************************************************/
AppId_t applicationId = new AppId_t(YOUR_APP_NUMBER_HERE);
```

Save and close the script

### steam\_appid.txt

Next you need to update the steam\_appid.txt used by the project.&#x20;

{% hint style="warning" %}
STOP\
\
Learn before you do, read our [article on steam\_appid.txt](../../../company/steam/steamworks/steam\_appid.txt.md) to understand what it is, why its used and when it should not be used.
{% endhint %}

You should find the steam\_appid.txt file in the root of your project but it will not be apart of your projects resources so you will need to look in your project folder.

Simply open the text file and update the App ID with your App ID
