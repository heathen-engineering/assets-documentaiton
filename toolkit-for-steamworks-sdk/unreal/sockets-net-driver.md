---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
---

# Sockets Net Driver

## Introduction

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

The Sockets Net Driver is a standard Unreal Net Driver designed to work with Valve's Steam Networking Sockets. It has a dependency on Online Subsystem Steam so it will install it and Online Subsystem if missing however that doesn't mean you have to use Online Subsystem if you don't want to.

## Addressing

The transport is technically capable of connecting through several different addressing methods including IP:Port however the most common and most valuable is to address via Steam ID.&#x20;

`steam.<SteamID>/<level_name>`

The above format is an example of how you would address a target connection using the Open Level node in Unreal's Blueprints

<figure><img src="../../.gitbook/assets/image (390).png" alt=""><figcaption><p>Convert a Hex ID to a Steam ID and use it as an address to connect to</p></figcaption></figure>

## Engine.ini

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
