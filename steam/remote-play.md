---
description: Remote local multiplayer
---

# 🛋 Remote Play

{% hint style="success" %}
#### Like what you're seeing?

Consider supporting us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% embed url="https://partner.steamgames.com/doc/features/remoteplay" %}

{% hint style="info" %}
The Steam documentation linked above is REQUIRED reading for Steam Remote Play.&#x20;

The system is very simple but does require a bit of configuration in your Steam Developer Portal.
{% endhint %}

Valve's Steam Remote Play lets you make a local multiplayer game that is also network multiplayer. It works in a manner similar to Steam game streaming ... that is the ability to play a game that is running on your PC but on your TV or other Steam Link device.

With Steam Remote Play you are running the game and your guest is streaming your game in that Steam Link similar manner. As far as your game is concerned the guest is a local player.

Once you have configured your game to work with Steam Remote Play you can use Heathen's [Remote Play API](../heathens-steamworks-complete/unity/api/remoteplay.client.md) to send invites, manage guests and generally make the most out of the feature in your game.

## Send an Invite

The first step to getting a remote play session going is to send an invite to a friend. The friend does not require a license to the game so you can send this invite to any friend. They will be streaming the game you are playing so it's your license of the game they will be playing on.

```csharp
if(API.RemotePlayClient.SendInvite(user))
    Debug.Log("Done");
else
    Debug.Log("Send failed");
```

When / if the guest connects the [Event Session Connected](../heathens-steamworks-complete/unity/api/remoteplay.client.md#session-connected) event will be invoked letting you know what the session ID is

## Get Session Data

Once a user has connected you might want to know which user it is, what form factor they are playing in or even what resolution they are running at. The Remote Play API has all of these and uses the Session ID the [Event Session Connected](../heathens-steamworks-complete/unity/api/remoteplay.client.md#session-connected) told you about.

```csharp
void HandleSessionConnected(SteamRemotePlaySessionConnected_t responce)
{
    session = responce.m_unSessionID;
}
```

With the session known, you can then

```csharp
//Get the UserData for the connected user
UserData user = API.RemotePlay.Client.GetSessionUser(session);
```

```csharp
//Get the name of the device the session is playing on
string clientName = API.RemotePlay.Client.GetSessionClientName(session);
```

```csharp
//Get the form factor the session is playing in
ESteamDeviceFormFactor formFactor = API.RemotePlay.Client.GetSessionClientFormFactor(session);
```

or

```csharp
//Get the resolution the session is playing at
Vector2Int resolution = API.RemotePlay.Client.GetSessionClientResolution(session);
```

## Player Controls

This is handled exactly as you do with a local player, as far as your game is concerned each of the "session guests" is a local player and is causing local inputs to occur e.g. controller input, keyboard/mouse input, etc. will all act as if local.

The whole idea of Steam's Remote Play is that if you created a local multiplayer game then this will simply work right out of the box with you needing to do nothing more than invite a player to remote play.
