---
description: The most important part
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Steamworks Behaviour

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Steamworks Behaviour simply initializes the Steam API for you and exposes common events to the Unity Inspector. As of version 2.30.12 Steamworks Behaviour no longer runs the callback loop. We have made it such that Steam API can be initialized and ran without using any component scripts. That said most uses cases will greatly benifit from using Steamworks Behaviour in their [bootstrap scene](../../../company/design/bootstrap-scene.md).

## Use

You should add a Steamworks Behaviour component to a game object in the first scene to be loaded by your game. It is important that this game object is never destroyed as it is operating your Steam API integration. We do recommend you use additive loading and simply never unload your [bootstrapping](../../../company/design/bootstrap-scene.md) scene however you can use the [Do Not Destroy](../../../company/design/bootstrap-scene.md) approach if you are carful to NEVER reload the scene that defined Steamworks Behaviour.

The Steamworks behaviour is not intended to be a functional component that is you will not interact with this component, it exists wholly to initialize, operate and shutdown the Steam API integration according to Unity events. The one exception to this case is when operating a Steam Game Server in a situation where you need to delay API initialization. You can optionally configure your Steam Settings to NOT auto initialize Steam Game Server, in which case you will need to call SteamworksBeahviour.InitializeGameServer in order to kick off the initialization process.

{% hint style="warning" %}
This is rare and in general you should be allowing the system to auto initialize.
{% endhint %}

```csharp
steamworksBeahviour.InitalizeGameServer();
```

## Events

### Evt Steam Initialized

```csharp
public UnityEvent evtSteamInitialized;
```

This is invoked when Steam API is fully initialized and all artifacts are ready for use.

This event has no parameters, a handler for this event would like:

```csharp
public void HandleEvent()
{
    //DO WORK
}
```

### Evt Steam Initialization Error

```csharp
public UnityStringEvent evtSteamInitializationError;
```

This is invoked if the Steam API fails to initialize.

This event has 1 parameter of type string which is a message indicating why it failed to initialize. A handler for this event would look like:

```csharp
public void HandleEvent(string errorMessage)
{
    //DO WORK
}
```

### Evt Lobby Invite Argument Detected

```csharp
public LobbyDataEvent evtLobbyInviteArgumentDetected;
```

This is invoked after initialization completes if the system detects a lobby ID was passed in on the command line arguments. This occurs when a user accepted a lobby invite but was not currently playing the game. In that use case Steam will launch the game with the lobby ID on the command line.&#x20;

This event has 1 argument of type [Lobby](../data-layer/lobby-data.md), being the lobby that was passed in on the command line argument and would have a handler that looks like:

```csharp
public void HandleEvent(Lobby lobby)
{
    //DO WORK
}
```

## Fields and Attributes

### Settings

```csharp
public SteamSettings settings;
```

The [SteamSettings ](../scriptable-objects/steam-settings/)that should be used when initializing the API.

## Methods

### Create If Missing

```csharp
public static void CreateIfMissing(SteamSettings settings, bool doNotDestroy = false)
```

A static method that can be used to create a Steamworks Behaviour safely on demand. It is not recommend to do this, you should be using a [Bootstrap scene](../../../company/design/bootstrap-scene.md) where the Steamworks Behaviour is set up at development time.&#x20;

If you choose or simply must use a "late initialization" approach then this method can be used to safely create the Steamworks Behaviour and optionally mark it as Do Not Destroy. Note this will not create anything if a Steamworks Behaviour already exists.
