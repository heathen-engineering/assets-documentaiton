---
description: How to .... everything!
---

# ⚙️ Steamworks

## Introduction

<figure><img src="../../../.gitbook/assets/Short Banner@2x.png" alt="Steamworks Complete"><figcaption></figcaption></figure>

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Complete</td><td><a href="https://github.com/sponsors/heathen-engineering">GitHub | Patreon</a></td><td><a href="https://www.unrealengine.com/marketplace/en-US/product/ad658ddf5c434478acb95f9091ea279c">Marketplace</a></td><td><a href="../../../.gitbook/assets/UnrealCardCover.png">UnrealCardCover.png</a></td><td><a href="../../../toolkit-for-steamworks/unreal/">unreal</a></td></tr><tr><td>Complete | Foundation</td><td><a href="https://github.com/sponsors/heathen-engineering">Gitub | Patreon</a></td><td><a href="https://assetstore.unity.com/packages/tools/integration/steam-api-steamworks-complete-246652">Asset Store</a></td><td><a href="../../../.gitbook/assets/UnityCardCover.png">UnityCardCover.png</a></td><td><a href="../../../toolkit-for-steamworks/unity/">unity</a></td></tr><tr><td>Foundation</td><td><a href="https://github.com/heathen-engineering/SteamworksFoundation">GitHub</a></td><td></td><td><a href="../../../.gitbook/assets/GodotCardCover.png">GodotCardCover.png</a></td><td><a href="broken-reference">Broken link</a></td></tr></tbody></table>

Heathen creates the top Steamworks integration for Unreal, Unity and is porting it to Godot! Want to do more with Valve's Steamworks SDK? Then check out [Heathen's Toolkit for Steamworks SDK](../../../toolkit-for-steamworks/steamworks.md)!

## Integrate

You will need to bring the Steamworks SDK assemblies into your project so you can make use of the features in your game logic.&#x20;

### Unity

#### [Toolkit for Steamworks SDK](../../../toolkit-for-steamworks/unity/)

The best way to get started quickly and Do More is with [Heathen's Toolkit for Steamworks SDK](../../../toolkit-for-steamworks/steamworks.md#feature-comparison) or if you are not quite sure yet you can start with the free "lite" version [Foundation](../../../toolkit-for-steamworks/steamworks.md#feature-comparison).

With Toolkit for Steamworks you can handle initialization and most features of Steamworks completely code-free. We also provide a robust set of tools for programmers greatly speeding up the process of integrating Steamworks with your project by providing robust and battle-tested systems and tools.&#x20;

#### Manual Integration

{% hint style="warning" %}
In general, you should never install anything to your project from a .unitypackage file.\
\
In particular, Steamworks.NET doesn't often update its unity package ... please do your self a massive favor and use UPM to install as described below
{% endhint %}

#### Install Steamworks.NET

First, you will need to Install Steamworks.NET, we recommend you do this via the Unity Package Manager and avoid installing it from the GitHub Release folder as that package is usually out of date and is not easily updated.

* From Git URL
  * Open the Unity Package Manager
  * Press the Add (+) button
  * Select Add from Git URL
  * Enter the URL \
    `https://github.com/rlabrecque/Steamworks.NET.git?path=/com.rlabrecque.steamworks.net`
* From Disk
  * Clone the Steamworks.NET Repo to your local disk ... we use GitHub Desktop for this.
  * Open the Unity Package Manager
  * Press the Add (+) button
  * Select Add from Disk
  * Browse to the `com.rlabrecque.steamworks.net` folder and import.

### Unreal

#### [Toolkit for Steamworks SDK](../../../toolkit-for-steamworks/unreal/)

The best way to get started quickly and Do More is with [Heathen's Toolkit for Steamworks SDK](../../../toolkit-for-steamworks/unreal/).

With Toolkit for Steamworks, you can access and leverage every aspect of Steamworks from Blueprint or C++ and we have created a number of Unreal-specific tools to simplify common use cases such as the Steam Save Game which is a classic Unreal Save Game that can leverage Steam's Cloud Storage as you would any normal Unreal Save Game.

#### Manual Install

You will need to include the Steam Shared Module. This is Unreal's built-in Third Party Engine Plugin that makes the Steamworks SDK available to your project. Sadly Unreal's built-in tools for Steamworks are very lacking so you will be using this from C++ as a raw API ... or you will want to use [Heathen's Toolkit for Steamworks](../../../toolkit-for-steamworks/unreal/) as talked about above.

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Initialize

### Unity

#### [Toolkit for Steamworks SDK](../../../toolkit-for-steamworks/unity/legacy/quick-start-guide/)

Our tools are built to support everyone, hobbyists, amateurs, pros, veteran engineers with decades of experience... and everything in between.

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3>Component</h3></td><td><ul><li>Zero Code</li></ul></td><td><a href="../../../.gitbook/assets/Screenshot 2023-01-30 111452.png">Screenshot 2023-01-30 111452.png</a></td><td><a href="../../../toolkit-for-steamworks/unity/legacy/quick-start-guide/gameobject-initialization.md">gameobject-initialization.md</a></td></tr><tr><td><h3>Object</h3></td><td><ul><li>Doesn't require a GameObject</li><li>Single line of code</li></ul></td><td><a href="../../../.gitbook/assets/Screenshot 2023-01-30 111537.png">Screenshot 2023-01-30 111537.png</a></td><td><a href="../../../toolkit-for-steamworks/unity/legacy/quick-start-guide/scriptableobject-initialization.md">scriptableobject-initialization.md</a></td></tr><tr><td><h3>API</h3></td><td><ul><li>Doesn't require a GameObject</li><li>No ScriptableObject</li><li>Pure C#</li></ul></td><td><a href="../../../.gitbook/assets/Screenshot 2023-01-30 111633.png">Screenshot 2023-01-30 111633.png</a></td><td><a href="../../../toolkit-for-steamworks/unity/legacy/quick-start-guide/api-initialization.md">api-initialization.md</a></td></tr></tbody></table>

#### Manual

{% hint style="danger" %}
[SteamManager.cs](https://github.com/rlabrecque/Steamworks.NET-Example/blob/master/Assets/Scripts/Steamworks.NET/SteamManager.cs) demonstrates this ... but you should not just copy and paste it blindly into your project.\
\
SteamManager.cs only initialize for the client API so it won't work with Steam Game Server, it also doesn't initialize input, leaderboards or other artefacts for you. \
\
It is ALWAYS important to read and understand and not simply copy example code snippets into your project expecting them to work.
{% endhint %}

If you are initializing Steam API for a client build you will need to register a handler on the `SteamAPIWarningMessageHook_t`, check the system is fit and ready to be initialized and then call the Init method of the SteamAPI static class.

```csharp
var result = Steamworks.SteamAPI.Init();
```

If this returns true then the API is initialized, otherwise it failed to initialize. Once initialized you will need to be sure you run callbacks each frame.

```csharp
Steamworks.SteamAPI.RunCallbacks();
```

If you are handling Steam Input you will probably want to update it as well with each frame though you can do that on demand.

### Unreal

#### [Toolkit for Steamworks SDK](../../../toolkit-for-steamworks/unreal/getting-started.md)

Create a new Game Instance derived from our Steam Game Instance ... or use the example BP\_SteamGameInstance as a jumping-off point.

<figure><img src="../../../.gitbook/assets/image (347).png" alt=""><figcaption></figcaption></figure>

Be sure to read over our Getting Started article for detailed instructions.

#### Manual

Keep in mind when working manually you are limited to Epic's assumptions ... which assumes you are only using Steam as part of an Online Subsystem. e.g. Online Subsystem Steam. Its configuration and initialization are part of the engine load process and are not available in PIE. [Hethen's Toolkit for Steamworks](../../../toolkit-for-steamworks/unreal/) does initialize Steam in PIE though of course some features do require you to run in standalone mode such as Overlay, Networking, etc.

Setting your App ID has two places in manual Unreal Steam config, In development, the OnlineSubsystemSteam SteamDevAppId value is used

```ini
[OnlineSubsystemSteam]
SteamDevAppId=480
```

For a build the define `UE_PROJECT_STEAMSHIPPINGID` is used. There are several ways to "define" this define.&#x20;

Using the PublicDefines list in your game's Build.cs&#x20;

```csharp
PublicDefinitions.Add("UE_PROJECT_STEAMSHIPPINGID=480");
```

Or in the GlobalDefines list in your game's Target.cs (**preferred**)

```csharp
GlobalDefinitions.Add("UE_PROJECT_STEAMSHIPPINGID=480");
```

To configure the plugin for proper initialization you will need to add the following to your Engine.ini

{% code fullWidth="false" %}
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
{% endcode %}

## Steam Debugging

{% hint style="info" %}
Steam's Documentation has a Debugging article as well ... read it ... its good

[https://partner.steamgames.com/doc/sdk/api/debugging](https://partner.steamgames.com/doc/sdk/api/debugging)
{% endhint %}

The following articles will help you learn how to perform common tasks and debug and troubleshoot your Steam API integration. We have created a large array of tools that simplify the use of Steam API including tools like Steamworks Inspector to help you troubleshoot and debug your integration.

## The Basics

### Steam must be running

Be aware that none of the work done by Steam API is "in" your game, Steam API is an "application program interface" that allows your game to work with features in the Steam client. As a result, you **must** have Steam client open, running and logged in to a valid Steam user who owns the app you are trying to work with.

The only exception to this is when using the [Steam Game Server](multiplayer/game-server-browser/) feature which also limits the functionality of Steam API as there is no client and no user available to do work.

### Running a Build&#x20;

When running a build that was not deployed to Steam and ran from the Steam client you will notice that the game fails to initialize the crashes to the desktop possibly attempting to re-launch from Steam client.

This is by design, you must hint to Steam API what the app is, read the [article on steam\_appid.txt](steam\_appid.txt.md) it will explain, why this happens, how to work with it, and when you should and when you should not use the feature described.

### Publish Your Changes

When you make any changes in the Steam Developer Portal you **must** publish them before they take effect and can be tested in your game

> Use this page to publish all of the metadata that you've used this site to author. You'll need to publish in order to test things like your game **depot configuration**, new builds, or new **achievements** you've added. If your game is not yet set to playable, this action **will not release the game**, but will simply **publish configuration changes you've made**.
>
> \
> The buttons below invoke source control (Perforce) commands - if you have any trouble with these, just let us know.

The above quote is from the publish page as seen below

![The publish page, make sure to publish before you try to test](<../../../.gitbook/assets/image (164).png>)

### Environment Checks

Having something wrong with your environment (Engine Editor, Steam.exe, Steam User, etc.) can cause odd issues with Steam API that are hard to pin down unless you know what to look for.

Here are some key things to check before you bother trying to debug anything.

### Steamworks.NET Install

{% hint style="info" %}
Issue present in Unity only
{% endhint %}

Did you **ever** have a manual or custom installation of Steamworks.NET or ever have any asset or tool that had such in your project?

That is at any time was there ever a Steamwork.NET in your project that was not from the Package Manager Git URL install?

If yes; then know that those custom installs would have Steamworks.NET artefacts in multiple folder locations. If that install was present or even partially present from an incomplete attempt to manually remove it then Unity will have ... on install of the proper Steamworks.NET from Package Manager ... attempted to merge the assets and made a complete mess of it.

#### How to fix

1. Remove the offending files\
   Steamworks.NET manual installs would have installed bits in several different folders (scripts, plugins, examples, etc.)\
   Many old assets would have buried a copy or customized version of Steamworks.NET in their asset.
2. Once you are positive that you fully removed Steamworks.NET and related files from your Assets folder.\
   Remove Steamworks.NET from the package manager and then reinstall it

### Steam Client Login

For some reason some devs like to run Steam.exe as Admin or run Unity Editor as Admin ... Windows will mangle your callbacks if you do this.

It's important that Unity Editor and Steam.exe are running as the same user, which should also be the user that is logged into the OS  in order for Steam API to work properly.

e.g. Do not run either Steam.exe or Unity Editor with elevated or any other non-standard permissions or users. If you do you will have issues.

### Steam User

Valve's Steam has a concept of "limited" users ... when a new user is created it is considered limited until it has spent the equivalent of 5 USD on the Steam store or added 5 USD to the Steam wallet.

This applies to dev accounts, publishers, etc. there are no exceptions. So if your account or your test account is new and or has not spent at least 5 USD on Steam odds are its limited by Valve and it will have limited access to Steam API including but not limited to&#x20;

* Lobby limits\
  Can join but can't really use a Steam Lobby ... this one is real odd as it will join it but it can't do anything beyond that
* Chat limits\
  Typically can't chat with anyone
* Friend limits\
  Typically can't have friends, friend chats, friend invites, etc.

In addition, the Steam User you're testing the game with MUST own a license to the app to initialize the Steam API. Developer accounts are "supposed" to be granted a dev license to the app ... however, we have seen it such that this doesn't happen correctly.

You can test and modify ownership of the app you are a dev for using Steam's command line as outlined in&#x20;

{% embed url="https://partner.steamgames.com/doc/sdk/api/debugging" %}

### Build Target

Steamworks.NET and as a result all related Steam code is only applicable to PC, Mac and Linux ... not Universal Windows or anything else ... ONLY ... Windows 32, Windows 64, Max OS and Linux 64 platforms.&#x20;

If your build target is set to ANY other build target then the Steamworks.NET assembly will not compile and will not be available for use.

#### What about multi-platform games?

use `#if DISABLESTEAMWORKS` script define you can add this yourself if you like to cause Steam API code to simply not compile. You can use it to strip out your Steam-related code if you need.

### Steam Command Line

{% embed url="https://partner.steamgames.com/doc/sdk/api/debugging" %}
Tools from Valve
{% endembed %}

> Steam has grown into a large application over the years and provides many separate modules and multiple different ways to debug. This page outlines as many of them as possible to help you get the most out of Steam and Steamworks while keeping headaches to a minimum.\
> \
> Steam automatically outputs a number of debug to the `logs` folder, for others you may need to use [Steam Command Line Parameters](https://partner.steamgames.com/doc/sdk/api/debugging#command\_line\_parameters) or [Steam Console Commands](https://partner.steamgames.com/doc/sdk/api/debugging#console\_commands) to enable them.\
> \
> Using [ISteamUtils::SetWarningMessageHook](https://partner.steamgames.com/doc/api/ISteamUtils#SetWarningMessageHook) allows a Steamworks application to register a function that allows the Steamworks API to provide human-readable error messages to the application when something goes wrong. Most Steam APIs use it, so be sure to hook it up and look at it any time something goes wrong.
