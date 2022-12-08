# Rich Presence



<figure><img src="../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Steam's Rich Presence is what populates all the details about a user in the Friends list and importantly for multiplayer games its what enables the "Join Game" button on the Steam friends list.

## Join Game Button

The Join Game button located on the Steam friends list in Steam client lets a user simply click a button and it will launch the game if its not already running and provide the game with connection details so it may join that player to their friends game.

What actually happens when a user presses that button is&#x20;

1. If the game is not already running
   1. Launch the game
   2. Provide the connect string as a command line parameter
2. If the game is already running
   1. Invoke the Game Rich Presence Join Requested event\
      You can find this event on [API.Overlay.Client](../../../api/overlay.md#game-rich-presence-join-requested) or by using the [Overlay Manager](../../components/overlay-manager.md#evtrichpresencejoinrequested)

## Enable

To enable the Join Game button on the Steam Friends list simply set the "connect" field of the user's rich presence.

{% embed url="https://partner.steamgames.com/doc/api/ISteamFriends#SetRichPresence" %}
Read more about Set Rich Presence and the connect field
{% endembed %}

```csharp
UserData.SetRichPresence("connect", connectionData);
```

This will set the local user's connect information to be whatever string you provide for connectionData. What exactly you should pass into as your connection data depends on how your game handles connection.

This would usually be the CSteamID of the server your playing on or the IP and Port if its using a traditional TCP/UDP connection or the CSteamID of the "Host" if your playing P2P.

### Disable

Simply clear the data

```csharp
UserData.SetRichPresence("connect", string.Empty);
```
