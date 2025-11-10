# Unreal Configuration

The Toolkit for Steamworks works with the Steamworks SDK and is compatible with all of Unreal's built-in Steam-related plugins. It uses the same configuration features to keep things simple. This means even if you are not using OnlineSubsystemSteam, you will be using its Engine.ini settings to configure and control the Toolkit for Steamworks.

### App ID

In development, the OnlineSubsystemSteam SteamDevAppId value is used

```ini
[OnlineSubsystemSteam]
SteamDevAppId=480
```

To define `UE_PROJECT_STEAMSHIPPINGID` we use the game's Target.cs, an example from one of our projects follows.

{% hint style="warning" %}
The following is just an example, you would use your own settings and the name of your constructor would of course be different. The point is to show you a working example in the Target.cs of your app.
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

<figure><img src="../.gitbook/assets/image (271).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You do not have to use the Online Subsystem Steam in order to do Steam Networking multiplayer. You will need to include and configure the plugin as that is how the Third Party Steam Shared plugin gets its config.\
\
You do not have to use Sessions or Advanced Sessions to work with it either, our tools enable you to use Steam Lobby and other standard Steamworks features as intended by Valve, without the confines of Epic's Online Subsystem \
\
You can of course, if you so wish, use Epic's Online Subsystem concept with Steam ... all options are supported.
{% endhint %}

We leverage the built-in Steam Socket Net Driver which has a dependency on the Online Subsystem Steam plugin. When you enable the Steam Sockets plugin (not just Online Subsystem Steam) the related dependencies should also be enabled and will require a restart of the engine.

Once enabled, the following ini settings become relevant ... learn more in Unreal's official documentation

{% embed url="https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine" %}

{% code fullWidth="false" %}
```ini
[URL]
; This is the Game Port that Steam Game Server will use, and by default should be 27017
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
; Should the Steam Shared and Online Subsystem Steam be enabled ... should always be true
bEnabled=True
; When Development Build, should RestartAppIfNecessary be checked and used should always be true
bRelaunchInSteam=True
; Should VAC be used, only applies to Steam Game Server
bVACEnabled=True
; Your AppID is only used for dev builds and in the editor
SteamDevAppId=480
; The game version ... this is only required if you are going to run a 
; Dedicated Server and have it visible over the Steam Game Server browser
GameVersion=1.0.0.0
; Query Port is by default 2017, this is only used by the Steam Game Server
GameServerQueryPort=27018
; If using Sessions, then you need this set to true, else you can ignore it
; bInitServerOnClient=true

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

## Game Instance

With the plugin installed, you will want to set up your Game Instance.&#x20;

The plugin ships with a ready-to-use Steam Game Instance named `BP_SteamGameInstance` You can use this as is, or use it as a learning tool to create your own Game Instance derived from our SteamGameInstance parent class, or use it as is.

### Global Events

Steamworks is largely a multi-process and thus asynchronous toolkit where you will need to listen to events to know when a request has been serviced. In many, if not most, cases, we provide a "Callback" parameter to methods where you can create an event that will be invoked for that specific method call.&#x20;

In some cases, however, you may wish to bind to the global event

<figure><img src="../.gitbook/assets/image (272).png" alt=""><figcaption></figcaption></figure>

To help you do this, we defined all of the global events as delegates on the Steam Game Instance and created a simple Get Steam Game Instance method that will fetch the current instance for you. You can then browse and bind to any events you like, be sure to unbind before the object in question leaves scope, as these are global events that remain in scope themselves for the life of your game.

<figure><img src="../.gitbook/assets/image (273).png" alt=""><figcaption><p>An example of binding an event</p></figcaption></figure>

## Callbacks

As you should know, Steamworks SDK enables your game to ask Steam (the authenticated client on the user's machine) to do stuff for your game. This means it is largely a multi-process and asynchronous thing.

Valve classically handles this using Callback and CallResult delegates. This is translated in Unreal as "Global" events and Function callbacks.

### Global Events

You can bind to global events via the Steam Game Instance ... we provide a simple Get Steam Game Instance node to make this easy to "get".

<figure><img src="../.gitbook/assets/image (272).png" alt=""><figcaption></figcaption></figure>

You can then browse and bind to any events you like, be sure to unbind before the object in question leaves scope, as these are global events that remain in scope themselves for the life of your game.

<figure><img src="../.gitbook/assets/image (273).png" alt=""><figcaption><p>An example of binding an event</p></figcaption></figure>

### Function Callbacks

These take the place of Valve's "CallResult" delegate and are scoped to a specific method call. For these, you will see there is a delegate parameter on the function call where you can create an event that will be invoked when the request is complete.

<figure><img src="../.gitbook/assets/image (274).png" alt=""><figcaption></figcaption></figure>

## Steam Developer

Become a Steam Developer and get your own App ID.

Valve does provide a test app ID you can use as a matter of demonstration, and our Steam Game Instance will default to its App ID (480); however, you will want to register for your own App ID as soon as possible.

You can learn more about [getting started as a Steam Developer in our article here](../register-with-valve.md)!

## Builds

If you are building a Dedicated Server, you will need to ensure you have the following definitions declared. There are several ways you can go about this, such as Target.cs, Please see Unreal Engine's documentation for details.

{% hint style="info" %}
This is a requirement from the Online Subsystem Steam plugin and deals with how it initializes the Steamworks SDK.

We document it here because it is often overlooked. To find the source documentation, please review the [Server Details](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine#serverdetails) section of the [Online Subsystem Steam article](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine) on Epic's documentation site.
{% endhint %}



You can use your game's Target.cs to set these values using the GlobalDefinitions list.

```csharp
GlobalDefinitions.Add("UE_PROJECT_STEAMSHIPPINGID=480");
GlobalDefinitions.Add("UE_PROJECT_STEAMGAMEDESC=Human Styled: Name");
GlobalDefinitions.Add("UE_PROJECT_STEAMGAMEDIR=FolderName");
GlobalDefinitions.Add("UE_PROJECT_STEAMPRODUCTNAME=480");
```

<table data-full-width="false"><thead><tr><th width="321">UE Macro</th><th width="195">Steam Name</th><th>Notes</th></tr></thead><tbody><tr><td><code>UE_PROJECT_STEAMPRODUCTNAME</code></td><td><code>STEAMPRODUCTNAME</code></td><td>Typically your App ID<br>Used by Steam Game Server Matchmaking features.</td></tr><tr><td><code>UE_PROJECT_STEAMGAMEDIR</code></td><td><code>STEAMGAMEDIR</code></td><td>This should be the folder where your game resides and is usually just the game name sans spaces and symbols. note it's just the folder name, not the path it's self</td></tr><tr><td><code>UE_PROJECT_STEAMGAMEDESC</code></td><td><code>STEAMGAMEDESC</code></td><td>Usually the human name of your game</td></tr><tr><td><code>UE_PROJECT_STEAMSHIPPINGID</code></td><td></td><td>This is 100% Unreal Engine and is used in both client and server when not in the editor or a Dev build. <br><br>It is simply your App ID and is used during initialization.</td></tr></tbody></table>

### steam\_appid.txt

We have a full article on what this text file is and when you should or should not be using it. Epic notes are similar in their article [here](https://dev.epicgames.com/documentation/en-us/unreal-engine/online-subsystem-steam-interface-in-unreal-engine#steamappid).

In short, this should only be needed when you're running a packaged project from outside of Steam or if your running a Dedicated server build.
