# Steam Lobby

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

Steam Matchmaking is driven primarily through the Steam Lobby feature. In a nutshell, the concept is that players will create a "lobby". You can think of this a bit like a chat room. This lobby has "metadata" associated with it which can be used to search for lobbies, filtering the results to just those the player cares about.‌

The metadata concept of Steam Lobby is where most of the functionality comes into play. The owner or "host" of a lobby can set the metadata on a lobby and anyone else can read that data, and the Steam Lobby search system can use that data to refine search results. In addition, each member within a lobby has a set of metadata associated with them. Lobby member metadata can only be set by the member it is related to and can only be read by other members of that lobby.‌

In summary lobby metadata is for stating the intent of the session or the status of the session and is accessible by everyone. Member metadata is for stating the intent of a member or the status of a member and is writable only by that member and readable only by fellow members of the same lobby.‌

You can read more about Steam's Matchmaking system on Valve's developer documentation.

{% embed url="https://partner.steamgames.com/doc/features/multiplayer#matchmaking" %}

## Use Cases

### Create a Lobby or Group.

For more information on lobby types see Valve's documentation [https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs](https://partner.steamgames.com/doc/api/ISteamMatchmaking#typedefs)&#x20;

See the [API.Matchmaking](../../api/matchmaking.md#create-lobby) interace for details on creating a lobby. In addition the [Lobby Manager](../../components/lobby-manager.md) tools can help you create, join and manage a lobby for a specific function in your game.&#x20;

Lets say for example you use 2 types of lobbies in your game

*   Party

    This would be where you have your player gather a group of friends together to play together i.e. a group or party as seen in MMOs, MOBA or really any game with a coop feature
*   Session Lobby

    This would be where you have your player's configure a game play session and wait for competitors to join or similar. This is the most typical use of a lobby and what drives matchmaking in your game.

In the above use case you would attack a [Lobby Manager](../../components/lobby-manager.md) to your Party UI and another to your Session UI. You would configure each accordingly and each can manage its own chat and metadata features. This helps you split functionality across concepts unique to your game.

### Find and Join Lobbies

The easiest way to search for and join lobbies is through the [Lobby Manager](../../components/lobby-manager.md) tool. Alternatively you can use Heathen's API.Matchmaking directly to easily search for and join lobbies.&#x20;

Aside from browsing for a lobby you can handle invite and joining of lobby invites. Inviting a friends to lobby can be done in a number of ways including from outside of your game via the Steam Friends list.

Internally to you game you can use the [User Data](../../objects/user-data.md) object to invite a specific player. You would have access to this object from various tools and interfaces including [Friends](../../api/friends.md), [Clans ](../../api/clans.md)and there related chat systems. When you send an invite it is up to that user to accept it and there are multiple use cases for how they might accept the invite

#### While In game

In this case the accepting user is already in game and so the Game Lobby Join Invite event will be raised on the [Overlay Manger](../../components/overlay-manager.md#events) and its related [API.Overlay](../../api/overlay.md#game-lobby-join-requested) interface.

#### While out of game

In this case the accepting user is not yet in game and so the Steam client will launch the game and pass as an argument on the command line the lobby connection information. It is up to you to handle this argument, navigate to the appropriate place iin your game e.g. the lobby UI and then join the lobby ID indicated on that argument.

A crude example follows

```csharp
// Return the ulong value of the lobby to join if any
public static ulong GetSteamLobbyInvite()
{
    var args = Environment.GetCommandLineArgs();
    ulong value = 0;
    for (int i = 0; i < args.Length; i++)
    {
        if (args[i] == CommonCommands.SteamLobbyConnect 
            && i + 1 < args.Length 
            && ulong.TryParse(args[i + 1], out value))
            return value;
    }

    return value;
}
```

Then you can perform the following

```csharp
var targetLobby = GetSteamLobbyInvite();
if(targetLobby > 0)
{
    //TODO: navigate to the Lobby UI in your game
    //Join the lobby
    API.Matchmaking.Client.JoinLobby(targetLobby);
}
```

### Using Lobby Chat

Steam's Lobby system includes a simple chat system able to handle text or data. The easiest way to interact with lobby chat is via the [Lobby Chat Director](../../components/lobby-chat-director.md) which needs to be added to the same object as your [Lobby Manager](../../components/lobby-manager.md).

You can also interact with lobby chat manually through the [API.Matchmaking](../../api/matchmaking.md) interface.

### Notify "Connect to network"

The typical purpose of a lobby is to gather player's and settle on the rules and conditions of the multiplayer session. In most cases you will at some point want to notify player's that they should connect to a particular server be that a Peer in a P2P game or a dedicated server on the net.

The lobby system provides tools for this via the `SetGameServer` method on the lobby

```csharp
public void Lobby.SetGameServer()

public void Lobby.SetGameServer(CSteamID gameServerId)

public void Lobby.SetGameServer(string address, ushort port)

public void Lobby.SetGameServer(string address,
                                ushort port,
                                CSteamID gameServerId)
```

{% hint style="warning" %}
The SetGameServer method can only be called by the "Owner" of the lobby
{% endhint %}

When called Valve will record the information on the Steam Lobby metadata as shown below

![](<../../../../.gitbook/assets/image (65).png>)

Each member of the lobby (other than the owner) will be notified by callback which raises the `EventLobbyGameCreated` event located on the [API.Matchmaking](../../api/matchmaking.md) interface and exposed through the [Lobby Manager](../../components/lobby-manager.md).&#x20;

{% hint style="warning" %}
All members of a lobby should upon joining the lobby register an event handler on the `Lobby.evtGameServerSet` event

```csharp
API.Matchmaking.EventLobbyGameCreated.AddListener(HandleGameServerSet);
```
{% endhint %}
