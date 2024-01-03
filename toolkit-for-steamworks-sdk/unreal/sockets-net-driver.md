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

`steam.<SteamID>/<level_name>`

The above format is an example of how you would address a target connection using the Open Level node in Unreal's Blueprints

<figure><img src="../../.gitbook/assets/image (390).png" alt=""><figcaption><p>Convert a Hex ID to a Steam ID and use it as an address to connect to</p></figcaption></figure>

## Engine.ini

Unreal requires you to specify the NetDriver you are using as part of the engine configuration ... this is commonly done in the Engine.ini

{% hint style="warning" %}
The specifics of your Engine.ini may change when installing the plugin as part of a project vs as an engine plugin such as from Marketplace
{% endhint %}

### System Settings

The first step is to configure the handshake version and set the session ID's to 0. If not done you will find the server fails to complete handshake on client connect and will reject messages from the client resulting in a disconnect.

### Engine

Clear the NetDriver definition and set NetSocketsNetDriver as our GameNetDriver.

### Net Sockets Net Driver

Configure the net driver timeout settings and define the connection class name.

`SteamworksComplete.NetSocketsNetDriver` is the formal name of the NetDriver and `SteamworksComplete.NetSocketsNetConnection` is the formal name of the connection class for example, assuming you have installed the plugin from GitHub as part of your project (e.g. a project plugin) your NetDriverDefinitions entry and Plugins config might take the form

{% hint style="success" %}
Note you should set the ConnectionTimeout and InitialConnectTimeout to a value that makes sense for you.\
\
In the example below we use 60 ... which is a very long timeout but can be useful for dev/test where we often test on very clunky and slow machines.

\
Production would probably be better set as a much smaller value 2-10 for example.
{% endhint %}

```ini
[SystemSettings]
net.CurrentHandshakeVersion=2
net.MinHandshakeVersion=2
net.VerifyNetSessionID=0
net.VerifyNetClientID=0

[/Script/Engine.Engine]
!NetDriverDefinitions=ClearArray
+NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="SteamworksComplete.NetSocketsNetDriver",DriverClassNameFallback="SteamworksComplete.NetSocketsNetDriver")

[/Script/SteamworksComplete.NetSocketsNetDriver]
ConnectionTimeout=60.0
InitialConnectTimeout=60.0
NetConnectionClassName="SteamworksComplete.NetSocketsNetConnection"

[Plugins]
EnabledPlugins=SteamworksComplete
```
