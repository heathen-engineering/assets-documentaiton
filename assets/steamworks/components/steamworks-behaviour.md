---
description: The most important part
---

# Steamworks Behaviour

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

Steamworks Behaviour replaces the concept of Steam Manager as seen in some of the older Steamworks.NET example scripts. This behaviour object deals with the initialization of the Steam API and operating its main update loop.&#x20;

{% hint style="danger" %}
Your game should have exactly one of these behaviours.

Your game should never destroy or reload one of these behaviours.



This means you should not define this behaviour in a scene that is loaded multiple times such as a title or menu scene.



You are **STRONGLY** encouraged to use a [bootstrap ](../../../company/concepts/fundamentals/bootstrap-scene.md)model taking advantage of Unity's multi-scene features. Alternatively you can use the Steamworks Creator behaviour.
{% endhint %}

## Use

You should add a Steamworks Behaviour component to a game object in the first scene to be loaded by your game. It is important that this game object is never destroyed as it is operating your Steam API integration. We do recommend you use additive loading and simply never unload your [bootstrapping](../../../company/concepts/fundamentals/bootstrap-scene.md) scene however you can use the [Do Not Destroy](../../../company/concepts/fundamentals/bootstrap-scene.md) approach if you are carful to NEVER reload the scene that defined Steamworks Behaviour.

The Steamworks behaviour is not intended to be a functional component that is you will not interact with this component, it exists wholly to initialize, operate and shutdown the Steam API integration according to Unity events. The one exception to this case is when operating a Steam Game Server in a situation where you need to delay API initialization. You can optionally configure your Steam Settings to NOT auto initialize Steam Game Server, in which case you will need to call SteamworksBeahviour.InitializeGameServer in order to kick off the initialization process.

{% hint style="warning" %}
This is rare and in general you should be allowing the system to auto initialize.
{% endhint %}

```csharp
steamworksBeahviour.InitalizeGameServer();
```

## FAQ

### Where are all the events?

We have created managers and events components which can be used not only to expose events to the Unity inspector but to provide game object based access to various systems.

#### [Lobby Chat Director](lobby-chat-director.md)

Exposes controls and events for a specific lobby chat

#### [Lobby Manager](lobby-manager.md)

Exposes controls and events for a specific lobby

#### [Overlay Manager](overlay-manager.md)

Exposes controls and events for the Steam Overlay features

#### [Steam System Events](steam-system-events.md)

Provides inspector access to Initialize and Initialization Error events

#### [Steam Game Server Events](steam-game-server-events.md)

Provides inspector access to connect, disconnect and failure events for the Steam Game Server system.
