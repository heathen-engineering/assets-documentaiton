---
description: The original
---

# Overlay Manager

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

## Introduction

The overlay manager provides access to overlay events such as activated and the lobby and game server join requests as well common methods such as opening the overlay to a target web page.

Everything done in this manage can be done via API.Overlay.

## Definition

### Fields and Attributes

| Type                  | Name                 | Comments                                                                            |
| --------------------- | -------------------- | ----------------------------------------------------------------------------------- |
| ENotificationPosition | NotificationPosition | Updates the notification position used by the Steam Client popup                    |
| Vector2Int            | NotificationInset    | Updates the pixel offset of the notificaiton positon used by the Steam Client popup |
| bool                  | IsShowing            | True when the overlay is showing                                                    |
| bool                  | IsEnabled            | True if the overlay feature of the Steam API is enabled by this user for this app   |



### Events

#### evtOverlayActivated

Occurs when the overlay is activated&#x20;

#### evtGameLobbyJoinRequested

Called when the user tries to join a lobby from their friends list or from an invite. The game client should attempt to connect to specified lobby when this is received. If the game isn't running yet then the game will be automatically launched with the command line parameter `+connect_lobby <64-bit lobby Steam ID>` instead.

#### evtGameServerChangeRequested

Called when the user tries to join a different game server from their friends list. The game client should attempt to connect to specified server when this is received

### Methods

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
