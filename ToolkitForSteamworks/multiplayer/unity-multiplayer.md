# Unity Multiplayer

This guide is designed to help Unity developers get started quickly with multiplayer game development using Steamworks. It covers the key concepts and architectures you need to know, including the distinction between high-level and low-level networking APIs, and how Steamworks integrates into the picture.

As to "How To" that is covered by the HLAPI you choose to use. Steamworks is a technology that enables capabilities ... capabilities that are used by the HLAPI you choose.

***

## Understanding the Networking Layers

### High-Level API (HLAPI)

* **What It Is:**\
  HLAPIs are frameworks that handle the replication of game state and data synchronisation. They define what gets synced, when, by whom, and how messages are transmitted across the network.
* **Popular Tools:**
  * [**FishNet**](https://fish-networking.gitbook.io/docs)\
    [Transport](https://fish-networking.gitbook.io/docs/manual/guides/components/transports/fishysteamworks)
  * [**Mirror**](https://mirror-networking.com/)\
    [Transport](https://github.com/Chykary/FizzySteamworks/)
  * [**NetCode for GameObjects**](https://docs-multiplayer.unity3d.com/netcode/current/about/)\
    [Transport](https://github.com/Unity-Technologies/multiplayer-community-contributions/tree/main/Transports/com.community.netcode.transport.steamnetworkingsockets)
  * [**PurrNet**](https://purrnet.gitbook.io/docs)\
    [Transport](https://purrnet.gitbook.io/docs/systems-and-modules/network-manager/transports/steam-transport)
* **Key Point:**\
  All these HLAPIs work similarly. Your choice of HLAPI is mostly a matter of "flavour" or personal preference. Once chosen, you’ll use its documentation for detailed implementation guidance.

### Low-Level API (LLAPI)

* **What It Is:**\
  Often referred to as the "transport" layer, LLAPIs handle the actual sending and receiving of data, managing connection details such as establishing, maintaining, and terminating network connections.
* **Steamworks Integration:**
  * The Steamworks SDK includes the **Steam Networking Sockets** protocol.
  * Major HLAPIs offer a transport module that supports Steam Networking Sockets.
* **Key Point:**\
  While LLAPIs manage the technical details of connections (think of them like “NetDrivers” in other engines), they operate behind the scenes. Once your HLAPI is configured with the proper transport, you use the HLAPI as usual with little to no changes in your workflow.

***

## Setting Up Your Multiplayer Architecture

### Choosing Your HLAPI and Transport

* **Step 1:**\
  Select an HLAPI that suits your project needs. Remember, the HLAPI handles most of the game’s network logic.
* **Step 2:**\
  Install the corresponding transport module that enables integration with Steam Networking Sockets. This configuration ensures that your HLAPI communicates using Steam’s protocols without affecting your standard development practices.

### General Network Architecture

* **Star Topology:**\
  Most Unity HLAPIs use a star topology managed by a central **Network Manager**. This manager handles all network connections, ensuring that data flow between clients and servers remains organised.
* **Server Types:**
  * **Listen Server:**\
    Often confused with P2P, a Listen Server is where one instance acts as both client and server. This is the proper term to use; some HLAPI may (incorrectly) refer to this as Peer to Peer, however, that term does mean something different to Valve, so understand outside of HLAPI's docs, P2P means something else.
  * **Dedicated Server:**\
    A dedicated server runs independently, handling connections from multiple clients. When initialising a dedicated server with Steamworks, it is assigned a Steam ID via Steam Game Server endpoints (handled by Heathen’s Toolkit for Steamworks).

***

## Key Steamworks Integration Points

### Steam ID as the Connection Address

* **Connection Method:**\
  All Unity HLAPIs using Steam Networking Sockets treat the Steam ID as the network address.
* **Implication:**\
  Instead of connecting via an IP:Port combination, connections are made directly between Steam IDs (for both users and servers). This is what Valve means when they say P2P ... between 2 of the same type of address, whether or not they are clients or servers or both.
* **Connect to ID:**\
  How you know the ID to connect to depends on the "discovery" method you choose for your game. Steamworks has quite a few tools that can help here
  * [Lobby](../features/lobby.md#invite-to-lobby)
  * [Game Server Browser](../features/steam-game-server.md)
  * [Rich Presence](../features/rich-presence.md#for-multiplayer-games)
  * [Friend Invite](../features/user.md#invite-to-game)
  * [Party Beacons](../features/party.md#create-beacon)
  * [Type in a Hex ID](../features/csteamid.md#toolkit-for-unity) (see tools to convert User IDs to and from Hex)

### Dedicated Servers and Steam IDs

* **Server Initialisation:**\
  Dedicated servers initialise using Steam Game Server endpoints, receiving a Steam ID. Heathen’s Toolkit for Steamworks automates this process in your server builds.

### The Role of Steam Lobby

* **Clarification:**
  * **Steam Lobby:** A tool primarily used for matchmaking. It helps players find each other and agree on session parameters.
  * **Networking:** Steam Lobby is **not** a networking feature.
* **Key Point:**\
  Once a network session is established, you connect directly using Steam IDs—not through the lobby. The lobby’s role ends once the session is set up.

***
