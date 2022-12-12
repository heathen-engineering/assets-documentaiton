# Overlay.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

```csharp
using API = HeathenEngineering.SteamworksIntegration.API;
```

```csharp
public static class API.Overlay
```

The whole of the overlay system is only accessible from the Client API as a result you will always be using the form:

```csharp
API.Overlay.Client
```

### What can it do?

The overlay interface provides simplified access to Steam's overlay features. The Steam Overlay can be used to show web pages, access friends lists, clans,&#x20;

### Related Componenets

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/overlay-manager" %}

## Events

### Game Overlay Activated

Called when the overlay activates or deactivates.

### Game Server Change Requested

Called when the user tries to join a different game server from there friends list while the game is running.

### Game Lobby Join Requested

Called when the user tries to join a lobby from there friends list or from an invite while the game is running.

### Game Rich Presence Join Requested

Called when the user tries to join a game from their friends list or after a user accepts an invite by a friend with `userData.InviteToGame(connectString);` or `API.Friends.Client.InviteUserToGame(user, connectString);`.

{% hint style="info" %}
This callback is made when joining a game. If the user is attempting to join a lobby, then the callback [Game Lobby Join Requested](overlay.md#game-lobby-join-requested) will be made.
{% endhint %}

## How To

### Enabled and showing

You can check if the Overlay is enabled ... that is ... is the overlay feature turned on for this app for this user.

```csharp
if(API.Overlay.Client.IsEnabled)
    Debug.Log("yes it is");
else
    Debug.Log("no it is not");
```

To check if the overlay is currently open you can use

```csharp
if(API.Overlay.Client.IsShowing)
    Debug.Log("yes it is");
else
    Debug.Log("no it is not");
```

### Notification positioning

The notification pop up that shows when a user unlocks and achievement or when friends join or leave games can be configured to show in different areas of the screen.

```csharp
API.Overlay.Client.NotificationPosition = 
        EnotificationPosition.k_EPositionTopRight;
        
API.Overlay.Client.NotificationInset = new Vector2Int(0,0);
```

### Activate the overlay

You can activate the overlay in a number of ways.

#### To a given dialog

```csharp
API.Overlay.Client.Activate(dialog);
```

#### To the lobby invite screen

```csharp
API.Overlay.Client.ActivateInviteDialog(lobbyId);
```

#### To a game connection

```csharp
API.Overlay.Client.ActivateInviteDialog(connectionInfo);
```

#### To remote play&#x20;

```csharp
API.Overlay.Client.ActivateRemotePlayInviteDialog(lobbyId);
```

#### To an app store page

```csharp
API.Overlay.Client.Activate(appId, flag);
```

#### To a user dialog

```csharp
API.Overlay.Client.Activate(dialog, user);
```

#### To a web page

```csharp
API.Overlay.Client.ActivateWebPage(url);
```
