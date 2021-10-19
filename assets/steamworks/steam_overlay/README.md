---
description: Working with the Steam Overlay.
---

# Overlay

{% hint style="info" %}
#### Code Documentation

[HeathenEngineering.SteamAPI.SteamSettings.GameClient.Overlay](https://heathen-engineering.github.io/steamworks-v2-documentation/#CSharpClass:HeathenEngineering.SteamAPI.SteamSettings.GameClient.Overlay)
{% endhint %}

{% hint style="warning" %}
In order to use the Steam Overlay the game must be built, deployed to Steam and launched from the Steam Client.&#x20;

Please note that Steam Overlay is not a feature inside your game, it is simply the Steam client rendering its overlay on top of your game's window. For this to work your game must be launched from Steam. If this does not work, it is not due to code in your game. Users may disable the Steam Overlay so you should not assume it is always available.
{% endhint %}

## Introduction

You can access the overlay object from code through the static accessors as seen below.

```csharp
SteamSettings.Client.overlay
```

The Steam Overlay is a feature of the Steam Client, and is used by Steam to display notifications to the user and to act as a quick access to Steam's social network features while the user is in game. For example Steam Friend Chat, Clan Chat, Broadcasting, Web Browser, Screenshots, Achievement notifications, events notifications, these are all presented to the user via the Steam Overlay while they are in a game.

As a game developer you can invoke the Steam Overlay from within your game. See the [Examples ](overlay\_examples.md)article for demonstrations of common use cases. Its important to note that a user can disable the Steam Overlay for a specific game or for all games so you shouldn't assume that the Overlay is there and available, the [Examples ](overlay\_examples.md)section shows how you can test for overlay availability.

## Configuration

The Steam Overlay's notification popup can be configured on a per game basis. That is you can indicate what corner the notification should show in and what offset if any. By default the notification popup will display in the lower right corner with a zero offset.

![](<../../../.gitbook/assets/image (67).png>)
