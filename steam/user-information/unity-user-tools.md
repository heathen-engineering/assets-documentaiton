---
cover: ../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Unity User Tools

## Clans (aka Groups)

The Steam Clan, aka Steam Group system, is part of Valve's Steam Friend system. Players can freely create clans which work similarly to guilds in MMOs in that they have a roster, and officers, can run events and have a dedicated chat system that is always accessible to members.

Heathen's Clan Tools simplify Valve's clan interface features. It maintains a list of the player's clans and each clan's membership which can be refreshed on demand. Clan chat can be interacted with through code, though in general it's advised to use the Steam Overlay as Clan chat can be very complex on account of the large number of users and that a player may interact with the chat from a wide range of sources such as Steam Client, Web Browser, Mobile App, Overlay or of 3rd party apps and games.

Heathen's tools like the [Clan List](../../toolkit-for-steamworks-sdk/unity/ui-components/clan-list.md), [Clan Chat Director](../../toolkit-for-steamworks-sdk/unity/ui-components/clan-chat-director.md) and more can help you bring the group/clan system in-game.

## Friends List

It is possible to chat with specific friends in the game though this is not typical. To get started you would need to enable the [Listen for Friend Messages](../../toolkit-for-steamworks-sdk/unity/api/friends.client.md#setlistenforfriendsmessages) feature in the [Friend API](../../toolkit-for-steamworks-sdk/unity/api/friends.client.md). Once this is enabled the [EventGameConnectedFriendChatMsg ](../../toolkit-for-steamworks-sdk/unity/api/friends.client.md#game-connected-friend-chat-msg)event will be raised when receiving a message from a friend. You can also [Send Messages](../../toolkit-for-steamworks-sdk/unity/data-layer/user-data.md#sendmessage) to friends either via the [User Data](../../toolkit-for-steamworks-sdk/unity/data-layer/user-data.md) object or the [Friend API](../../toolkit-for-steamworks-sdk/unity/api/friends.client.md).

## User Data

The Heathen framework simplifies the concept of Steam User Data in our [UserData](../../toolkit-for-steamworks-sdk/unity/data-layer/user-data.md) object. This object is equitable and comparable to CSteamID and ulong meaning you can convert any CSteamID or ulong value to a UserData object.

```csharp
UserData user_fromUlong = 1234566;
UserData user_fromCSteamID = new CSteamID(1234566);
UserData user = UserData.Get(1234566);
```

This means you no longer need to "Get" a UserData object as you did in other steam integrations. The UserData object exposes all relevant information about the user in question with simple fields.&#x20;

{% hint style="info" %}
For full details see [UserData's documentation here](../../toolkit-for-steamworks-sdk/unity/data-layer/user-data.md).
{% endhint %}

### Local User

The most common use case is to fetch the local user's information. This can be done with a single line call.

```csharp
using HeathenEngineering.SteamworksIntegration.API;

// ...

var localUser = User.Client.Id;
```

For example if you wanted to get the local user's name as it appears on Steam.

```csharp
using HeathenEngineering.SteamworksIntegration.API;

// ...

var userName = User.Client.Id.Name;
```

### Avatar Image

Unlike previous iterations we only load the image when requested, this saves memory usage by only loading avatars that are requested.

```csharp
using HeathenEngineering.SteamworksIntegration.API;

// ...

if(User.Client.Id.Avatar != null)
{    
    // The avatar is already loaded
}
else
{
    User.Client.Id.LoadAvatar((result) => 
    {
        //Result will be the avatar if we could load it else null
    });
}
```

Note the Avatar field checks for loaded avatar images and returns the matching image if found.

The LoadAvatar method does similar but asynchronously and will load the image if not found. It does this by taking an Action as a parameter and invoking it when the image is found or loaded as required.

If your not aware of what a callback is see this [article](../../guides/development/lambda-expressions.md#callbacks).

### Display User information

There are a few pre-made components that can help display common UserData to the screen such as the [Set User Avatar](../../toolkit-for-steamworks-sdk/unity/ui-components/set-user-avatar.md) and [Set User Name](../../toolkit-for-steamworks-sdk/unity/ui-components/set-user-name.md) components. These simply set uGUI RawImage or uGUI Text or TMPro text fields.&#x20;
