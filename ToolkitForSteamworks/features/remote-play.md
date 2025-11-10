# Remote Play

[Steam Remote Play](https://partner.steamgames.com/doc/features/remoteplay) allows you to turn a **local multiplayer game** into a **network-enabled experience**, without rewriting your game for online networking. It works similarly to Steam Link or game streaming: your game runs on your machine, and your friend streams it remotely while interacting with it as if they were sitting beside you.

As far as your game is concerned, **remote guests are local players**. Steam handles the streaming, input, audio, and video over the network, allowing multiple people to play together even if only one of them owns the game.

{% embed url="https://partner.steamgames.com/doc/features/remoteplay" %}

***

## Core Concept

When you start a Remote Play session, Steam acts as the bridge:

* You (the host) run the game.
* Steam streams the game to your invited friend(s).
* Guest inputs (e.g., controllers, keyboard, mouse) are sent back to your game as **local input events**.

Your game doesn’t know or care that these players are remote—it only sees input from connected devices. This means if your game already supports couch co-op or local multiplayer, **Remote Play will “just work”** with minimal effort.

***

## Configuration Required

To use Remote Play, you need to:

* Enable the **Remote Play Together** feature in the Steamworks developer portal for your app.
* Mark your game as supporting local multiplayer or co-op.
* Ensure input handling in your game is already designed for multiple players sharing the same system.

Once this is done, you can start leveraging the Remote Play API to interact with sessions.

***

## Session Workflow

Here’s how a typical Remote Play flow works:

1. **Send an Invite:**\
   You can invite any Steam friend to join your session—even if they don’t own the game. The game runs on your machine; they stream it to you.
2. **Session Connected Event:**\
   When the guest accepts the invite, your game will be notified of a new Remote Play session. This event includes a **Session ID**, which you’ll use to reference that player in further API calls.
3. **Query Session Data:**\
   Once connected, you can:
   * Identify the Steam user.
   * Check their device type (TV, tablet, etc.).
   * Get screen resolution.
   * Adjust game settings accordingly.
4. **Player Input Handling:**\
   From your game’s perspective, input from a remote guest is **indistinguishable** from local input. Steam routes its input through virtual controllers or keyboards, so your existing local player logic remains unchanged.

***

## Examples

### Send an Invite

The first step to getting a remote play session going is to send an invite to a friend. The friend does not require a license to the game so you can send this invite to any friend. They will be streaming the game you are playing so it's your license of the game they will be playing on.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Not Applicable

## C\#

```csharp
// Be ready to listen when they accept
RemotePlay.Client.EventSessionConnected.AddListener(HandleSessionConnected);

// To invite a player
if (RemotePlay.Client.SendInvite(User))
    Debug.Log("Done");
else
    Debug.Log("Send failed");
```

When or if the guest connects the Event Session Connected even will be invoked letting you know what the session ID is.

```csharp
private void HandleSessionConnected(SteamRemotePlaySessionConnected_t Callback)
{
    // You should store this somewhere as you will use it later.
    session = Callback.m_unSessionID;

    // Get the UserData for the connected user
    UserData user = RemotePlay.Client.GetSessionUser(session);

    // Get the name of the device the session is playing on
    string clientName = RemotePlay.Client.GetSessionClientName(session);

    // Get the form factor the session is playing in
    ESteamDeviceFormFactor formFactor = RemotePlay.Client.GetSessionClientFormFactor(session);

    //Get the resolution the session is playing at
    Vector2Int resolution = RemotePlay.Client.GetSessionClientResolution(session);
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Coming Soon

<figure><img src="../.gitbook/assets/image (184).png" alt=""><figcaption><p>Usage Nodes</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (185).png" alt=""><figcaption><p>Global Events</p></figcaption></figure>

## C++

Coming Soon
{% endtab %}

{% tab title="Steamworks.NET" %}
Coming Soon
{% endtab %}
{% endtabs %}

### Player Controls

This is handled exactly as you do with a local player, as far as your game is concerned, each of the "session guests" is a local player and is causing local inputs to occur, e.g. controller input, keyboard/mouse input, etc., will all act as if local.

The whole idea of Steam's Remote Play is that if you created a local multiplayer game, then this will simply work right out of the box with you needing to do nothing more than invite a player to remote play.
