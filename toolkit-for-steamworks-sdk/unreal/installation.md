---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Installation

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=vxZ0jvBi0s8" %}
Video is silent but does have subtitles/captions
{% endembed %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><h3>GitHub Sponsor</h3></td><td><p><a href="https://github.com/sponsors/heathen-engineering">Become a Sponsor</a></p><p><em>The link below only works for Sponsors</em><br><a href="https://github.com/heathen-engineering/SourceRepo">Installation Instructions</a></p><p>Cancel anytime, and keep everything you have including our site-based license</p><ul><li>$15.00 month</li><li>Source Access<br>For all our assets</li><li>Live Updates</li><li>Exclusive extras</li><li>Issue Tracking</li><li>Escalated Live Support</li><li><p>Unity</p><ul><li>Toolkit for Steamworks</li><li>PhysKit Complete</li><li>UX Complete</li></ul></li><li><p>Unreal</p><ul><li>Toolkit for Steamworks</li></ul></li></ul></td><td></td></tr><tr><td><h3>Unreal Marketplace</h3></td><td><p><a href="https://www.unrealengine.com/marketplace/en-US/product/ad658ddf5c434478acb95f9091ea279c">Unreal Marketplace</a></p><ul><li>$74.99</li><li>Source Included</li><li>Quarterly Updates<br>+ Hotfixes</li><li>Toolkit for Steamworks</li><li>Live Support</li></ul></td><td><mark style="color:orange;">Per-user license, free updates for that major version, discount on future major updates</mark></td></tr></tbody></table>

## Requirements

### Version

You'll need to install Unreal v5.1 and later

### SteamShared

You will need to include the Steam Shared plugin.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

When adding the plugin from the marketplace it will be installed as an Engine plugin and should add its dependencies automatically.

If you are importing the plugin to your project as opposed to as an engine plugin it is advisable to add the SteamShared plugin first. If you forget before you add the plugin, you can adjust the .uproject manually by adding `SteamShared` to the list of plugins

```json
{
	"FileVersion": 3,
	"EngineAssociation": "5.2",
	"Category": "",
	"Description": "",
	"Modules": [
		{
			"Name": "ProjectName",
			"Type": "Runtime",
			"LoadingPhase": "Default"
		}
	],
	"Plugins": [
		{
			"Name": "ModelingToolsEditorMode",
			"Enabled": true,
			"TargetAllowList": [
				"Editor"
			]
		},
		{
			"Name": "SteamShared",
			"Enabled": true
		}
	],
	"TargetPlatforms": [
		"Linux",
		"Mac",
		"Windows"
	]
}
```

### C++

You'll need your project to support C++\
No this doesn't mean you have to use C++, but the engine needs to have the project headers and build process of compiling from C++. So you need to do that.

If you chose a C++ project when you created your project congratz, step done, and move on.

If you chose Blueprint project when you created your project, simply add a C++ class via the Tools menu and Unreal Editor will do the work of setting your project up so it can be completed.

## Installation

### From the Marketplace

The plugin is deployed to the Unreal Marketplace as an engine plugin. This means you need to install the plugin to the engine after purchase in order to be able to use it.

<figure><img src="../../.gitbook/assets/image (367).png" alt=""><figcaption></figcaption></figure>

Once you have installed the plugin to the engine versions you require you need to enable the plugin for your project, this will require a restart to complete.

<figure><img src="../../.gitbook/assets/image (368).png" alt=""><figcaption></figcaption></figure>

### From GitHub

The plugin will be installed as part of your project as opposed to part of the engine. To get started close your engine, and navigate to the project folder, this is where your .uproject file is located.

You should see a .sln file beside it, if you do not then your project is not set up for C++ so go back a step and fix that.

Once you do have a .sln we need to copy the Plugins in. You may already have a Plugins folder if not simply create one.

#### Add the plugin

Next, copy the SteamworksComplete folder into your Plugins folder. You'll find the plugin in our GitHub Sponsor Source Repo

<figure><img src="../../.gitbook/assets/image (30) (1) (1).png" alt=""><figcaption></figcaption></figure>

When done your folder should look similar to the above.

#### Modify the Plugin configuration

If you do not own the Plugin from the Unreal Marketplace then the Epic editor will see that this plugin is also a Marketplace plugin and expect you to download it from there

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

You have 2 options to sidestep this, 1 you could deploy it as an engine plugin (personly not my preference) or you can modify the SteamworksComplete.uplugin to empty the `MarkeplaceURL` node, as shown below

```ini
{
    ...
    "MarketplaceURL": "",
    ...
}
```

#### Generate files

Next, right-click on the .uproject file and select Generate Visual Studio project files

<figure><img src="../../.gitbook/assets/image (369).png" alt=""><figcaption></figcaption></figure>

#### Rebuild

Right-click on your projects .uproject file and select `Generate Visual Studio Project files`. This will cause the engine to scan the project directory and link up all the related bits we just copied in.

## Configuration

{% hint style="info" %}
### New to v2

v2 is in preview with GitHub Sponsors and Patreons, it will be released to Unreal Marketplace #Soon™️
{% endhint %}

Toolkit for Steamworks works with Steamworks SDK and is compatible with all of Unreal's built-in Steam-related plugins. It uses the same configuration features to keep things simple. This means even if you are not using OnlineSubsystemSteam you will be using its Engine.ini settings to configure and control Toolkit for Steamworks.

### App ID

In development, the OnlineSubsystemSteam SteamDevAppId value is used

```ini
[OnlineSubsystemSteam]
SteamDevAppId=480
```

For a build the define `UE_PROJECT_STEAMSHIPPINGID` is used. There are several ways to "define" this define. using the PublicDefines list in your game's Build.cs is a common approach.

```csharp
PublicDefinitions.Add("UE_PROJECT_STEAMSHIPPINGID=480");
```

### Steam Sockets

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

We leverage the built-in Steam Socket Net Driver which has a dependency on the Online Subsystem Steam plugin. When you enable Steam Sockets plugin (not just Online Subsystem Steam) the related dependencies should also be enabled and will require a restart of the engine.

Once enabled the following ini settings become relevant ... learn more in Unreal's official documentation

{% embed url="https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine" %}

```ini
[URL]
; This is the Game Port that Steam Game Server will use and by default should be 27017
Port=27017

[SystemSettings]
; Need this to sort out handshake issues with 5.1 and 5.2
net.CurrentHandshakeVersion=2
net.MinHandshakeVersion=2
net.VerifyNetSessionID=0
net.VerifyNetClientID=0

[OnlineSubsystem]
; Let the Online Subsystem know which platform you are working with
DefaultPlatformService=Steam

[OnlineSubsystemSteam]
bEnabled=True
; Should VAC be used, only applies to Steam Game Server
bVACEnabled=True
; Your AppID only used for dev builds and in the editor
SteamDevAppId=480
; The game version ... this is only required if you are going to run a 
; Dedicated Server and have it visible over Steam Game Server browser
GameVersion=1.0.0.0
; Query Port is by default 2017 this is only used by Steam Game Server
GameServerQueryPort=27018
; If using Sessions then you need this set to true, else you can ignore it
bInitServerOnClient=true

[/Script/Engine.GameEngine]
; Clear existing definitions
!NetDriverDefinitions=ClearArray
; Add the Steam Sockets Net Driver
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="/Script/SteamSockets.SteamSocketsNetDriver",DriverClassNameFallback="/Script/SteamSockets.SteamNetSocketsNetDriver")

[/Script/OnlineSubsystemSteam.SteamNetDriver]
; Set the Connection class name for the net driver
NetConnectionClassName="/Scripts/SteamSockets.SteamSocketsNetConnection"
```
