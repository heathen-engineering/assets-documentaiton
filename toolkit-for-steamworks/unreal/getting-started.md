---
cover: ../../.gitbook/assets/Unreal Banner.jpg
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

# Getting Started

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## [Installation](installation.md)

{% hint style="info" %}
Be sure to read the [Installation ](installation.md)article, it contains information on initial engine and project configuration that will prevent most "getting started" issues.
{% endhint %}

Import the Toolkit for Steamworks plugin to your project. Whether you purchased the plugin from Unreal Marketplace or are a GitHub Sponsor you will need access to the Toolkit for Steamworks plugin to get started using it.

The plugin is not free and is only available from Heathen via the [GitHub Sponsor](../../where-to-buy/become-a-sponsor.md) program, [Patreon ](https://www.patreon.com/HeathenEngineering)and on the [Unreal Marketplace](https://www.unrealengine.com/marketplace/en-US/product/ad658ddf5c434478acb95f9091ea279c). If you acquired the plugin anywhere else we suggest you remove it immediately as it's not a legit copy and likely contains malware.&#x20;

## Configuration

Toolkit for Steamworks works with Steamworks SDK and is compatible with all of Unreal's built-in Steam-related plugins. It uses the same configuration features to keep things simple. This means even if you are not using OnlineSubsystemSteam you will be using its Engine.ini settings to configure and control Toolkit for Steamworks.

### App ID

In development, the OnlineSubsystemSteam SteamDevAppId value is used

```ini
[OnlineSubsystemSteam]
SteamDevAppId=480
```

To define `UE_PROJECT_STEAMSHIPPINGID` we use the game's Target.cs, an example from one of our projects follows.

{% hint style="warning" %}
The following is just an example you would use your own settings and the name of your constructor would of course be different. The point is to show you a working example in the Target.cs of your app.
{% endhint %}

```csharp
public TuathaLegendsTarget(TargetInfo Target) : base(Target)
{
    Type = TargetType.Game;
    DefaultBuildSettings = BuildSettingsVersion.V5;
    IncludeOrderVersion = EngineIncludeOrderVersion.Latest;

    //Set our app id
    ProjectDefinitions.Add("UE_PROJECT_STEAMSHIPPINGID=1024120");
    //Set our human-friendly name
    ProjectDefinitions.Add("UE_PROJECT_STEAMGAMEDESC=Túatha: Legends");
    //Set our directory name
    ProjectDefinitions.Add("UE_PROJECT_STEAMGAMEDIR=TuathaLegends");
    //Set the product name
    ProjectDefinitions.Add("UE_PROJECT_STEAMPRODUCTNAME=1024120");
    //Add our module name
    ExtraModuleNames.AddRange( new string[] { "TuathaLegends" } );
}
```

### Steam Sockets

<figure><img src="../../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You do not have to use Online Subsystem Steam in order to do Steam Networking multiplayer. You will need to include and configure the plugin as that is how the Third Party Steam Shared plugin gets its config.\
\
You do not have to use Sessions or Advanced Sessions to work with it either, our tools enable you to use Steam Lobby and other standard Steamworks features as intended by Valve without the confines of Epic's Online Subsystem \
\
You can of course if you so wish, use Epic's Online Subsystem concept with Steam ... all options are supported.
{% endhint %}

We leverage the built-in Steam Socket Net Driver which has a dependency on the Online Subsystem Steam plugin. When you enable Steam Sockets plugin (not just Online Subsystem Steam) the related dependencies should also be enabled and will require a restart of the engine.

Once enabled the following ini settings become relevant ... learn more in Unreal's official documentation

{% embed url="https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine" %}

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

## [Game Instance](game-instance.md)

With the plugin installed, you will want to set up your Game Instance.&#x20;

The plugin ships with a ready-to-use Steam Game Instnace named `BP_SteamGameInstance` You can use this as is or use it as a learning tool to create your own Game Instnace derived from our SteamGameInstance parent class or use it as is.

### Global Events

Steamworks is largely a multi-process and thus asynchronous toolkit where you will need to listen on events to know when a request has been serviced. In many if not most cases we provide a "Callback" parameter to methods where you can create an event that will be invoked for that specific method call.&#x20;

In some cases, however, you may wish to bind to the global event

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

To help you do this we defined all of the global events as delegates on the Steam Game Instance and created a simple Get Steam Game Instance method that will fetch the current instance for you. You can then browse and bind on any events you like, be sure to unbind before the object in question leaves scope as these are global events that remain in scope themselves for the life of your game.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>An example of binding an event</p></figcaption></figure>

## Callbacks

As you should know Steamworks SDK enables your game to ask Steam (the authenticated client on the user's machine) to do stuff for your game. This means it is largely a multi-process and asynchronous thing.

Valve handles this in a classic way using Callback and CallResult delegates. This is translated in Unreal as "Global" events and Function callbacks.

### Global Events

You can bind to global events via the Steam Game Instance ... we provide a simple Get Steam Game Instance node to make this easy to "get".

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

You can then browse and bind on any events you like, be sure to unbind before the object in question leaves scope as these are global events that remain in scope themselves for the life of your game.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>An example of binding an event</p></figcaption></figure>

### Function Callbacks

These take the place of Valve's "CallResult" delegate and are scoped to a specific method call for these you will see there is a delegate parameter on the function call where you can create an event that will be invoked when the request is complete.

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## [Steam Developer](../../company/steam/quick-start.md#sign-up-to-steamworks)

Become a Steam Developer and get your own App ID.

Valve does provide a test app ID you can use as a matter of demonstration and our Steam Game Instance will default to its App ID (480) however you will want to register for your own App ID as soon as possible.

You can learn more about [getting started as a Steam Developer in our article here](../../company/steam/quick-start.md)!

## Builds

If you are building a Dedicated Server you will need to ensure you have the following definitions declared, there are several ways you can go about this such as the Target.cs, please see Unreal Engine's documentation for details.

{% hint style="info" %}
This is a requirement from the Online Subsystem Steam plugin and deals with how it initializes the Steamworks SDK.

We document it here because it is often overlooked, to find the source documentation please review the [Server Details](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine#serverdetails) section of the [Online Subsystem Steam article](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine) on Epic's documentation site.
{% endhint %}



You can use your game's Target.cs to set these values using the GlobalDefitnions list.

```csharp
GlobalDefinitions.Add("UE_PROJECT_STEAMSHIPPINGID=480");
GlobalDefinitions.Add("UE_PROJECT_STEAMGAMEDESC=Human Styled: Name");
GlobalDefinitions.Add("UE_PROJECT_STEAMGAMEDIR=FolderName");
GlobalDefinitions.Add("UE_PROJECT_STEAMPRODUCTNAME=480");
```

<table data-full-width="false"><thead><tr><th width="321">UE Macro</th><th width="195">Steam Name</th><th>Notes</th></tr></thead><tbody><tr><td><code>UE_PROJECT_STEAMPRODUCTNAME</code></td><td><code>STEAMPRODUCTNAME</code></td><td>Typically your App ID<br>Used by Steam Game Server Matchmaking features.</td></tr><tr><td><code>UE_PROJECT_STEAMGAMEDIR</code></td><td><code>STEAMGAMEDIR</code></td><td>This should be the folder where your game resides and is usually just the game name sans spaces and symbols. note it's just the folder name, not the path it's self</td></tr><tr><td><code>UE_PROJECT_STEAMGAMEDESC</code></td><td><code>STEAMGAMEDESC</code></td><td>Usually the human name of your game</td></tr><tr><td><code>UE_PROJECT_STEAMSHIPPINGID</code></td><td></td><td>This is 100% Unreal Engine and is used in both client and server when not in the editor or a Dev build. <br><br>It is simply your App ID and is used during initialization.</td></tr></tbody></table>

### steam\_appid.txt

We have a [full article](../../company/steam/steamworks/steam\_appid.txt.md) on what this text file is and when you should or should not be using it. Epic notes are similar in their article [here](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine#steamappid).

In short, this should only be needed when your running a packaged project from outside of Steam or if your running a Dedicated server build.

## Use the kit

The Example Level presents a UI that demonstrates key features

<figure><img src="../../.gitbook/assets/image (412).png" alt=""><figcaption></figcaption></figure>

Be sure to check out the Graph on the BP\_Example\_UI for additional examples such as how to find, join and create a Steam Lobby, Host and Join a network session via Steam Networking Sockets, etc.

{% hint style="info" %}
The Center Bottom text boxes are used to test lobby and multiplayer features.&#x20;

### Lobby

* You can create a lobby by clicking the button with the input field empty.
* You can join a lobby by typing in the Hex ID of the lobby you wish to join.&#x20;
* Browsing and matchmaking can also be done with blueprint nodes only, we simply didn't want to clutter the example with to many use cases.

### Multiplayer


{% endhint %}

Everything in the example scene is done with Blueprint Nodes requiring no C++ work at all. The UI WIdgets used are all created using Blueprint Nodes only again no C++ work required at all.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Features

Be sure to see the [Steamworks Guide](../../company/steam/steamworks/) and its sub-articles for more detail, follows is a quick list of major features you will find.

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Achievements</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>API</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>Authentication</td><td><a href="../../company/steam/steamworks/multiplayer/authentication.md">authentication.md</a></td></tr><tr><td>Cloud Save</td><td><a href="../../steam/cloud-save.md">cloud-save.md</a></td></tr><tr><td>Debugging</td><td><a href="../../company/steam/steamworks/#steam-debugging">#steam-debugging</a></td></tr><tr><td>Downloadable Content</td><td></td></tr><tr><td>Friend List</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>Input</td><td><a href="../../steam/input.md">input.md</a></td></tr><tr><td>Inventory</td><td><a href="../../company/steam/steamworks/inventory/">inventory</a></td></tr><tr><td>Item Store</td><td><a href="broken-reference">Broken link</a></td></tr><tr><td>Leaderboards</td><td><a href="../../company/steam/steamworks/leaderboard-object/">leaderboard-object</a></td></tr><tr><td>Lobby</td><td><a href="../../company/steam/steamworks/multiplayer/matchmaking-tools.md">matchmaking-tools.md</a></td></tr><tr><td>Matchmaking</td><td><a href="../../company/steam/steamworks/multiplayer/matchmaking.md">matchmaking.md</a></td></tr><tr><td>Microtransactions</td><td><a href="../../steam/inventory/microtransactions.md">microtransactions.md</a></td></tr><tr><td>Multi-Platform Project</td><td><a href="../../company/steam/steamworks/multi-platform-project.md">multi-platform-project.md</a></td></tr><tr><td>Multiplayer</td><td><a href="../../company/steam/steamworks/multiplayer/">multiplayer</a></td></tr><tr><td>Rich Presence</td><td><a href="../../company/steam/steamworks/multiplayer/rich-presence.md">rich-presence.md</a></td></tr><tr><td>Room Systems</td><td><a href="../../company/steam/steamworks/multiplayer/room-systems.md">room-systems.md</a></td></tr><tr><td>Running a Build</td><td><a href="../../company/steam/steamworks/running-a-build.md">running-a-build.md</a></td></tr><tr><td>Steam Game Server</td><td><a href="../../company/steam/steamworks/multiplayer/game-server-browser/">game-server-browser</a></td></tr><tr><td>steam_appid.txt</td><td><a href="../../company/steam/steamworks/steam_appid.txt.md">steam_appid.txt.md</a></td></tr><tr><td>Steam ID</td><td><a href="../../steam/csteamid.md">csteamid.md</a></td></tr><tr><td>Stats</td><td><a href="../../company/steam/steamworks/stats-object.md">stats-object.md</a></td></tr><tr><td>User Information</td><td><a href="../../company/steam/steamworks/user-information/">user-information</a></td></tr><tr><td>Voice</td><td><a href="../../steam/voice.md">voice.md</a></td></tr><tr><td>Workshop</td><td><a href="../../company/steam/steamworks/workshop/">workshop</a></td></tr></tbody></table>

Beyond samples we have extensive documentation including how-to guides for nearly every aspect of the Steam platform, going beyond simple documentation for our tools and assets. You can learn more about all the features of Steam in our knowledge base by reviewing the hundreds of articles linked in the navigation panel to the left 👀

<figure><img src="../../.gitbook/assets/image (371).png" alt=""><figcaption></figcaption></figure>

If you have any questions simply look up ... there you will find our Search tool which is AI-assisted and fairly useful as well as links to our [Discord Community](https://discord.gg/6X3xrRc) where you can get live support.

## Troubleshooting

### Package Closes/Crashes on launch

This happens when you run a package that has not been deployed by the Steam client. You will find that the Should Restart event if you simply copied the example implementation closes the app if it has not been launched from the Steam client.

[See more here.](game-instance.md#should-restart)

You can prevent this check by adding a steam\_appid.txt to the root of your project as shown in the image below

{% hint style="warning" %}
DO NOT ship your game with steam\_appid.txt this bypass is meant for devs.

You DO want your game to shut down and relaunch from the Steam client to ensure the Steam API works properly in every other use case.

[Learn more about steam\_appid.txt and when to and when not to use it.](../../company/steam/steamworks/steam\_appid.txt.md)
{% endhint %}

### Editor Crash on Play

Where the crash log mentions an Access Violation or similar low-level exception noting the steam\_api.dll or a similar Steam-related assembly.

Typically caused by an issue with the Steam Shared plugin. This is a built-in plugin of the Unreal engine not part of Heathen's codebase but is a dependency. If you attempted to update Steamworks SDK or made some change to the engine build that prevents the Steam Shared plugin from loading properly you will get this sort of crash.

To correct the issue start by verifying your engine install, if you are building from source check for compilation errors and changes to the Third Party Steamworks engine plugin. If you installed via the launcher you can simply right-click on the engine version and select Verify, it will clean and correct any issues found.

### Callbacks are not working in the package

In most cases, this is due to Steam API not initializing,&#x20;

In most cases, with a package, this is due to you running the package without deploying it from the Steam client without using the steam\_appid.txt and without properly handling the [Restart Required](game-instance.md#should-restart) case.

When you run the package Steam API will perform a check known as "Restart Required" This checks to see if the app was run from the Steam client, if it was not it will attempt to re-launch the game from the Steam client.

If you are just getting started however your game won't have launch options in the Steam client so that will do nothing.

In addition, Steam API will not have initialized and will not be processing callbacks e.g. Steam API is simply not working in that case.

You can sidestep the Restart Required check by using the [steam\_appid.txt](../../company/steam/steamworks/steam\_appid.txt.md), please read and understand what steam\_appid.txt is before you use it.

### The Game Doesn't Stop (in the editor)

When you run your game in the editor, the editor's process (as far as Steam is concerned) is your game, so it will show it as "playing" as long as the Editor remains open. Attempting to force it to stop may close your editor unexpectedly or cause an Editor crash.

It doesn't hurt anything for Steam to see the Unreal Editor process as your game so you can simply ignore this.

If it bothers you, you can run the simulation as a Standalone Process from the editor, as this is its own process Steam will properly see it start and stop and the Overlay will work properly. Keep in mind if you have already ran in the editor you may need to restart the editor to get Steam to let go of that old initialization.

### Overlay Doesn't Work

Your probably running the simulation in the editor as opposed to as a separate process. The Steam Overlay works by finding the window handle of the window process that initialized it. When your running the simulation as part of the Editors process you will have issues with Overlay because Unreal Editor has a great many window handles most of which do not update every frame and so Steam Overlay just doesn't work properly.

If you run your app as a Standalone Process Overlay should work for you, though if you have already initialized in the editor you may need to restart to clear that initialization. See my game doesn't stop when I stop the simulation.

### On Launch 2 Windows Open

You are running your package without having deployed it from the Steam client.

You have configured launch options for your app

You are not handling the [Restart Required](game-instance.md#should-restart) case properly.

When you run the package Steam API will perform a check known as "Restart Required" This checks to see if the app was run from the Steam client, if it was not it will attempt to re-launch the game from the Steam client.

In addition, Steam API will not have initialized and will not be processing callbacks e.g. Steam API is simply not working in that case.

You can sidestep the Restart Required check by using the [steam\_appid.txt](../../company/steam/steamworks/steam\_appid.txt.md), please read and understand what steam\_appid.txt is before you use it.
