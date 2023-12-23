---
cover: ../../.gitbook/assets/Unreal Banner@2x.png
coverY: 0
---

# Sockets Net Driver

## Introduction

{% hint style="info" %}
The Sockets Net Driver is currently in preview and only available to GitHub Sponsors. If you have any questions please reach out to us on Discord (link in the top menu)
{% endhint %}

The Sockets Net Driver is a standard Unreal Net Driver designed to work with Valve's Steam Networking Sockets. Inspired by Unreal's built-in Net Driver Sockets but without dependency on an Online Subsystem. Steam Networking Sockets is a powerful UDP-like socket layer that can be used for classic "peer to peer" or "client / server" topologies.&#x20;

## Addressing

The transport is technically capable of connecting through several different addressing methods including IP:Port however the most common and most valuable is to address via Steam ID.&#x20;

`steam.12345678987654321`

or

`12345678987654321`

The above shows an example of addresses formed when working with the Steam Net Driver, the custom URL prefix `steam.` is optional if present or if the provided address is numeric it will be treated as a Steam ID

## Engine.ini

{% hint style="info" %}
This is a poorly documented aspect of the Unreal engine. Heathen is working with the community to explore and document this and other undefined features as we have for Valve's Steamworks.\
\
This is a WIP
{% endhint %}

Unreal requires you to specify the NetDriver you are using as part of the engine configuration ... this is commonly done in the Engine.ini

{% hint style="warning" %}
The specifics of your Engine.ini may change when installing the plugin as part of a project vs as an engine plugin such as from Marketplace
{% endhint %}

### Class Name

`SteamworksComplete.NetSocketsNetDriver` is the formal name of the NetDriver and `SteamworksComplete.NetSocketsNetConnection` is the formal name of the connection class for example, assuming you have installed the plugin from GitHub as part of your project (e.g. a project plugin) your NetDriverDefinitions entry and Plugins config might take the form

```ini
[/Script/Engine.Engine]
!NetDriverDefinitions=ClearArray
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="SteamworksComplete.NetSocketsNetDriver",DriverClassNameFallback="SteamworksComplete.NetSocketsNetDriver")

[/Script/SteamworksComplete.NetSocketsNetDriver]
NetConnectionClassName="SteamworksComplete.NetSocketsNetConnection"

[Plugins]
EnabledPlugins=SteamworksComplete
```
