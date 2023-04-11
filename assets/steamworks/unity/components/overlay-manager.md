---
description: The original
---

# Overlay Manager

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

The overlay manager provides access to overlay events such as activated and the lobby and game server join requests as well common methods such as opening the overlay to a target web page.

Everything done in this manage can be done via API.Overlay.

## Events

### evtOverlayActivated

Occurs when the overlay is activated&#x20;

Example handler

```csharp
public void HandleEvent(bool isOpen)
{
    if(isOpen)
        Debug.Log("Overlay is open");
    else
        Debug.Log("Overlay is closed");
}
```

### evtGameLobbyJoinRequested

Called when the user tries to join a lobby from their friends list or from an invite. The game client should attempt to connect to specified lobby when this is received. If the game isn't running yet then the game will be automatically launched with the command line parameter `+connect_lobby <64-bit lobby Steam ID>` instead.

Example handle

```csharp
public void HandleEvent(LobbyData lobby, UserData user)
{
    //the lobby is the lobby your where invited to
    //the user is who invited you
}
```

### evtGameServerChangeRequested

Called when the user tries to join a different game server from their friends list. The game client should attempt to connect to specified server when this is received

```csharp
public void HandleEvent(string address, string password)
{
    //Server address (e.g. "127.0.0.1:27015", "tf2.valvesoftware.com")
    //The password if any
}
```

### evtRichPresenceJoinRequested

Called when the user accepts a Rich Precense invite such as API.Friends.Client.InviteToGame(...); This is not an invite to a lobby, this is an invite to a game.

```csharp
public void HandleEvent(UserData fromFriend, string connectionString)
{
    //Here is who invited this user
    //Whatever connection string the inviting user passed in
}
```

## Fields and Attributes

### NotificationPosition

```csharp
public ENotificationPosition NotificationPosition { get; set; }
```

This discribes the position of the notification popups used by Steam client. options include

* k\_EPositionTopLeft
* k\_EPositionTopRight
* k\_EPositionBottomLeft
* k\_EPositionBottomRight

### NotificationInset

```csharp
public Vector2Int NotificationInset { get; set; }
```

This discribes the number of pixels to be offset from the indicated Notification Position

### IsShowing

```csharp
public bool IsShowing => get;
```

Is the overlay being displayed

### IsEnabled

```csharp
public bool IsEnabled => get;
```

Is the overlay enabled i.e. can it be shown

## Methods

### Open Overlay

```csharp
public void Open(string dialog);
```

or

```csharp
public void Open(OverlayDialog dialog);
```

Opens the Steam client overlay to the indicated dialog

```csharp
public void OpenLobbyInvite(CSteamID lobbyId);
```

Opens the Steam client overlay to the invite dialog for the indicated lobby

```csharp
public void OpenConnectStringInvite(string connecitonString);
```

{% hint style="danger" %}
Undocumented, Valve has not yet documented this feature, we are simply assuming
{% endhint %}

Open the Steam client overlay to an invite for a given Game Server

```csharp
public void OpenRemotePlayInvite(CSteamID lobbyId);
```

{% hint style="danger" %}
Undocumented, Valve has not yet documented this feature, we are simply assuming
{% endhint %}

Open the Steam client overlay to an invite for a given remote play session

```csharp
public void OpenStore(AppId_T appId, EOverlayToStoreFlag flag);
```

Opens the Steam client overlay to the store page of the indicated app with flags to modify the behaviour.

```csharp
public void OpenUser(string dialog, UserData user);
```

or

```csharp
public void OpenUser(FriendDialog dialog, UserData user);
```

Opens the Steam client overlay to the indicated user dialog

```csharp
public void OpenWebPage(string url);
```

Opens the Steam client overlay to the indicated web page
