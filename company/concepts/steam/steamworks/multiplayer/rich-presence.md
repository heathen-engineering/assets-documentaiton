# Rich Presence

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../">Guides and Tutorials</a></td><td><a href="../../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../../assets/physkit/">physkit</a></td><td><a href="../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../../assets/ux/">ux</a></td><td><a href="../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

Steam's Rich Presence is what populates all the details about a user in the Friends list and importantly for multiplayer games its what enables the "Join Game" button on the Steam friends list.

## Join Game Button

The Join Game button located on the Steam friends list in Steam client lets a user simply click a button and it will launch the game if its not already running and provide the game with connection details so it may join that player to their friends game.

What actually happens when a user presses that button is&#x20;

1. If the game is not already running
   1. Launch the game
   2. Provide the connect string as a command line parameter
2. If the game is already running
   1. Invoke the Game Rich Presence Join Requested event\
      You can find this event on [API.Overlay.Client](../../../../../assets/steamworks/api/overlay.md#game-rich-presence-join-requested) or by using the [Overlay Manager](../../../../../assets/steamworks/unity/components/overlay-manager.md#evtrichpresencejoinrequested)

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
