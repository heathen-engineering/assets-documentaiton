# Unreal Multiplayer

This guide explains how to get started with multiplayer in Unreal using Heathen's Toolkit for Steamworks. Unreal's networking is built into the engine, and our Toolkit streamlines the integration of matchmaking and lobby functionality without relying on outdated session systems.

***

## Leveraging Unreal’s Built-In Networking

### Structured Networking Architecture

* **Native Integration:**\
  Unreal Engine incorporates robust networking features as a core part of its architecture. This means much of the multiplayer logic is inherent to the engine.
* **Toolkit Advantages:**\
  Heathen's Toolkit for Steamworks allows you to work directly with Steam matchmaking and related tools. This integration eliminates the need for third-party session systems for most projects.

### Sessions vs. Direct Connection

* **Sessions & Advanced Sessions:**\
  Although Unreal supports Sessions and Advanced Sessions, we do not recommend using them. They make assumptions that can conflict with Steam Lobby functionalities and do not fully leverage the benefits of Steam’s matchmaking tools.
* **Direct Connection Method:**\
  Instead of sessions, you can use Unreal’s built-in **Open Level** node for connecting to a session. Simply use the "address" parameter as the level name to connect to the desired server.&#x20;

***

## Connecting and Hosting Multiplayer Sessions

### Connecting to a Session

<figure><img src="../.gitbook/assets/image (288).png" alt=""><figcaption></figcaption></figure>

* **Using Open Level:**
  * **Process:**\
    To connect to a session, call the Open Level node in your Blueprint and provide the target level name as the “address.” This method replaces the traditional session connection workflow.
  * **Toolkit Integration:**\
    Heathen's Toolkit for Steamworks handles the background work of connecting via Steam’s networking. For detailed connection flows, refer to our separate article on Steam Lobby.
  * **Connect to ID:**\
    How you know the ID to connect to depends on the "discovery" method you choose for your game. Steamworks has quite a few tools that can help here
    * [Lobby](../features/lobby.md#invite-to-lobby)
    * [Game Server Browser](../features/steam-game-server.md)
    * [Rich Presence](../features/rich-presence.md)
    * [Friend Invite](../features/user.md)
    * [Party Beacons](../features/party.md)
    * [Type in a Hex ID](../features/csteamid.md#toolkit-for-unreal) (see tools to convert User IDs to and from Hex)

### Starting a Listen Server

<figure><img src="../.gitbook/assets/image (289).png" alt=""><figcaption></figcaption></figure>

* **Listen Server Setup:**
  * **Procedure:**\
    For hosting a multiplayer game as a Listen Server, use the Open Level node. In the level options, append `?listen` to the level name. This instructs Unreal to launch the level in listen server mode.
  * **Underlying Mechanics:**\
    The addition of `?listen` ensures that your game instance acts as both a client and a server, enabling others to join your session.

***

## Key Steamworks Integration Considerations

#### Steam ID Connection Paradigm

* **Connecting via IDs:**
  * **Direct Connection:**\
    In Steam, you connect directly to a User or Server ID, not to a Lobby. This is crucial as it differs from Unreal's concept of session-based networking.
  * **Steam Lobby Role:**\
    For matchmaking, groups, etc., Steam Lobby is a separate tool. It helps players find each other and set up sessions, but it is not used for the actual network connection.
  * **Recommendation:**\
    We encourage you to review our dedicated article on Steam Lobby to fully understand its role and limitations.

***
