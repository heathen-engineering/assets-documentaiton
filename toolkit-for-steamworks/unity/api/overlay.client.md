---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Overlay.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

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

### Related Components

{% content-ref url="../components/overlay-manager.md" %}
[overlay-manager.md](../components/overlay-manager.md)
{% endcontent-ref %}

## Events

### Event Game Overlay Activated

Called when the overlay activates or deactivates.

```csharp
public static GameOverlayActivatedEvent EventGameOverlayActivated;
```

Handler takes the form of

```csharp
void HandleEvent(bool activated)
{
    //Do Work
}
```

### Event Game Server Change Requested

Called when the user tries to join a different game server from there friends list while the game is running.

```csharp
public static GameServerChangeRequestedEvent EventGameServerChangeRequested;
```

Handler takes the form of

```csharp
void HandleEvent(string server, string password)
{
    //Do Work
}
```

### Event Game Lobby Join Requested

Called when the user tries to join a lobby from there friends list or from an invite while the game is running.

```csharp
public static GameLobbyJoinRequestedEvent EventGameLobbyJoinRequested;
```

Handler takes the form of

```csharp
void HandleEvent(LobbyData lobby, UserData friend)
{
    //Do Work
}
```

### Event Game Rich Presence Join Requested

Called when the user tries to join a game from their friends list or after a user accepts an invite by a friend with `userData.InviteToGame(connectString);` or `API.Friends.Client.InviteUserToGame(user, connectString);`.

{% hint style="info" %}
This callback is made when joining a game. If the user is attempting to join a lobby, then the callback [Game Lobby Join Requested](overlay.client.md#game-lobby-join-requested) will be made.
{% endhint %}

```csharp
public static GameRichPresenceJoinRequestedEvent EventGameRichPresenceJoinRequested;
```

Handler takes the form of

```csharp
void HandleEvent(UseerData friend, string connectionString)
{
    //Do Work
}
```

## Fields and Attributes

### Is Enabled

True if the overlay feature is enabled for this user on this app

```csharp
public static bool IsEnabled => get;
```

### Is Showing

True if the overlay is currently open

```csharp
public static bool IsShowing => get;
```

### Notification Position

Can be set to adjust where the notificaiton position anchors from

```csharp
public static ENotificationPosition NotificationPosition { get; set; }
```

### Notification Inset

Offset from the position anchor

```csharp
public static Vector2Int NotificationInset { get; set; }
```

## Methods

### Activate

Open the overlay to the indicated target

```csharp
//Open to a specific Steam dialog by name
public static void Activate(string dialog);
```

or

```csharp
//Open to a specific Steam dialog by enum
public static void Activate(OverlayDialog dialog);
```

or

```csharp
//Opens the overlay to an indicated app with the indicated "flags"
public static void Activate(AppData appID, EOverlayToStoreFlag flag);
```

or

```csharp
//Opens the overlay to a specific dialog by name with context
public static void Activate(string dialog, CSteamID steamId);
```

or

```csharp
//Opens the overlay to a specific dialog by enum with context
public static void Activate(FriendDialog dialog, CSteamID steamId)
```

### Activate Invite Dialog

Opens the invite dialog&#x20;

```csharp
//Invites will be regarding this lobby
public static void ActivateInviteDialog(LobbyData lobbyId);
```

or

```csharp
//Invites will be regarding this connection string
public static void ActivateInviteDialog(string connectionString);
```

### Activate Remote Play Invite Dialog

Opens the remote play invite dialog with respect to a given lobby

```csharp
public static void ActivateRemotePlayInviteDialog(LobbyData lobbyId);
```

### Activate Web Page

Opens the overlay to a given web page

```csharp
public static void ActivateWebPage(string url);
```

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
