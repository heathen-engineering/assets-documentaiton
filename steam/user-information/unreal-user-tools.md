---
cover: ../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
---

# Unreal User Tools

## Rich Presence

You can use the [Clear Rich Presence](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/clear-rich-presence.md), [Set Rich Presence](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/set-rich-presence.md), [Get User Rich Presence](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-user-rich-presence.md), [Get User Rich Presence Key by Index](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-user-rich-presence-key-by-index.md) and [Get Rich Presence](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-rich-presence.md) to work with Steam's Rich Presence system in Unreal Blueprints.

## User Data

### User ID

Valve's Steam ID is a complex value made up of several parts, we outline this in detail [here](../csteamid.md). Heathen's [Steam ID Tools](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/steam-id-tools.md) provide functions for converting between Friend ID aka Account ID and the larger Steam ID as well as tools for converting Friend ID to and from a hexadecimal value.

### Avatar

The [Get My Steam Avatar](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-my-steam-avatar.md) and [Get User Steam Avatar](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-user-steam-avatar.md) nodes can be used to get the related user's avatar as a Texture 2D. A simple image widget [BP\_SteamAvatarImage](../../toolkit-for-steamworks-sdk/unreal/widgets/bp\_steamavatarimage.md) uses these nodes to further simplify the process of displaying a user's avatar image on screen.

### Name

The [Get Persona Name](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-persona-name.md), [Get Friend Persona Name](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-friend-persona-name.md) and [Get Player Nickname](../../toolkit-for-steamworks-sdk/unreal/blueprint-nodes/functions/get-player-nickname.md) nodes can be used to read the local user's name or another Steam user's name or nickname.

{% hint style="info" %}
A nickname is a name that the local user has applied to another user. For example, if your brother is on your friends list you might give them the nickname of Bro ... this nickname is only visible to you and you do not have a nickname for yourself.
{% endhint %}

A simple label widget [BT\_SteamUserName](../../toolkit-for-steamworks-sdk/unreal/widgets/bp\_steamusername.md) uses these nodes to further simplify the process of displaying a user's name to the screen.
