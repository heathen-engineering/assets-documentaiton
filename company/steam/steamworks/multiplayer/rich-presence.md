# 🧑🔧 Rich Presence

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Steam's Rich Presence is what populates all the details about a user in the Friends list and importantly for multiplayer games, it's what enables the "Join Game" button on the Steam friends list.

## Join Game Button

The Join Game button located on the Steam friends list in the Steam client lets a user simply click a button and it will launch the game if it's not already running and provide the game with connection details so it may join that player to their friends game.

What happens when a user presses that button is&#x20;

1. If the game is not already running
   1. Launch the game
   2. Provide the connect string as a command line parameter
2. If the game is already running
   1. Invoke the Game Rich Presence Join Requested event\
      You can find this event on [API.Overlay.Client](../../../../heathens-toolkit-for-steamworks-sdk/unity/api/overlay.client.md#game-rich-presence-join-requested) or by using the [Overlay Manager](../../../../heathens-toolkit-for-steamworks-sdk/unity/components/overlay-manager.md#evtrichpresencejoinrequested)

## Enable

To enable the Join Game button on the Steam Friends list simply set the "connect" field of the user's rich presence.

{% embed url="https://partner.steamgames.com/doc/api/ISteamFriends#SetRichPresence" %}
Read more about Set Rich Presence and the connected field
{% endembed %}

```csharp
UserData.SetRichPresence("connect", connectionData);
```

This will set the local user's connect information to whatever string you provide for connectionData. What exactly you should pass into as your connection data depends on how your game handles the connection.

This would usually be the CSteamID of the server you are playing on, or the IP and Port if it's using a traditional TCP/UDP connection or the CSteamID of the "Host" if you are playing P2P.

### Disable

Simply clear the data

```csharp
UserData.SetRichPresence("connect", string.Empty);
```
