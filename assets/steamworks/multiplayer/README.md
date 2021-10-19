---
description: Tools and features to help you create great multiplayer experances
---

# Multiplayer Tools

## Introduction

The Steam API includes a number of tools to empower your multiplayer games on the Steam platform. Heathen Engineering's integration take these further and help you integrate them deeply with your game project. In the package you will find `MatchmakingTools` , `SteamGameServer` tools for instantiation and browsing and integrations with popular 3rd party networking APIs via our `transports` .&#x20;

Heathen has also included lobby tools on the `Steamworks Inspector` debugging tool that will show you in detail the members, metadata and status of all lobbies you are connected to.

![Screen shot of the Steamworks Inspector Lobbies tab](<../../../.gitbook/assets/image (36).png>)

## Features

### Matchmaking

A set of tools to help you create, find and manage Steam lobbies rather your creating a group/party system or handling session lobbies the `MatchmakingTools` can help you do more!

Learn more at the page below

{% embed url="https://kb.heathenengineering.com/assets/steamworks/multiplayer/matchmaking-tools" %}

### Steam Game Server

Heathen Engineering's `Steamworks Behaviour` handles the Steam API for both the Client and Game Server interfaces, and does so automatically based on the build target of your project. Put simply that means we will initialize the Game Server APIs with headless / server builds and the Client APIs with regular builds.&#x20;

Learn more about Steam Game Server configuration at the page below

{% embed url="https://kb.heathenengineering.com/assets/steamworks/steam-settings#build-options" %}

### Networking

Steam API includes several powerful network interfaces suitable for peer to peer and client server based network architectures. These interfaces leverage Valve's backend network eleminating the need for NAT punch, routing services and similar. Steam Networking APIs use CSteamIDs to make connections as opposed to IP and Port offering an additional level of security and anonimity to your players in that there are no IP addresses or ports to leak.

Heathen has worked with both Mirror and MLAPI to insure community transports that effectivly leverage the Steam Networking APIs are available and compatable with Heathen's Steamworks. For more information please consult the [installation article](../../bgsdk/bgsdk-install.md).

{% embed url="https://kb.heathenengineering.com/assets/steamworks/installation#networking-integrations" %}
