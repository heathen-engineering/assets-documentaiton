---
description: Examples and use cases for the Steam Overlay system
---

# Examples

## Introduction

You can access the overlay from a number of placeses throughout the SDK. For general overlay features you can use the overlay member of the client object

```csharp
SteamSettings.Client.overlay
```

You can find more examples in the [code documentation](https://heathen-engineering.github.io/steamworks-v2-documentation/#CSharpClass:HeathenEngineering.SteamAPI.SteamSettings.GameClient.Overlay) for the Overlay object.

## Is the Overlay enabled

This checks to see if the Overlay can be used at all and you should check this before attempting to use it.

```csharp
if(SteamSettings.Client.overlay.IsEnabled)
    Debug.Log("Overlay is available for use");
else
    Debug.Log("Overlay is NOT available for use");
```

## Is the Overlay open

This checks to see if the overlay is currently open.

```csharp
if(SteamSettings.Client.overlay.IsOpen)
    Debug.Log("Overlay is currently open");
else
    Debug.Log("Overlay is NOT currenntly open");
```

## Open a friend's profile

### Via the Overlay object

```csharp
SteamSettings.Client.overlay.OpenProfile(userId);
```

### Via a User Data object

This assumes you have a [UserData ](../user-data.md)object named `userData`

```csharp
userData.OpenProfile();
```

## Invite a friend to a lobby

### Via the Overlay object

```csharp
SteamSettings.Client.overlay.Invite(lobbyId);
```

### Via a Lobby object

This assumes you are in a lobby and will be inviting the user to the normal lobby. Please see the [Matchmaking](../multiplayer/matchmaking-tools.md) section for more details

```csharp
MatchmakingTools.normalLobby.InviteUserToLobby(userId);
```

## Open the game's Workshop

Note you will need the desired game's App ID as we will be using the Open Web Page feature to navigate to the workshop. Simply replace `<ID>` in the string below to&#x20;

`https://steamcommunity.com/app/480/workshop/`&#x20;

The above would be the Workshop for App ID 480 (Spacewar) however that app is hidden so that URL shoudln't work. &#x20;

```csharp
SteamSettings.Client.overlay.OpenWebPage(
    "https://steamcommunity.com/app/<ID>/workshop/");
```

## Open the store to a game or DLC

For this you need the game or DLC's App ID. This can be useful for showing a DLC store in your game and opening the Steam store from there. Note you can load the app into the user's cart optionally.

```csharp
SteamSettings.Client.overlay.OpenStore(
    AppId, 
    EOverlayToStoreFlag.k_EOverlayToStoreFlag_AddToCartAndShow);
```

## Open the offical game group

```csharp
SteamSettings.Client.overlay.OpenOfficialGameGroup();
```

## Open the game stats

### Via the Overlay object

```csharp
SteamSettings.Client.overlay.OpenStats();
```

### Via a User Data object

This assumes you have a [UserData ](../user-data.md)object named `userData` and will open the stats to this user's stats entry if available to the user making the call e.g. if this user is a friend.

```csharp
userData.OpenStats();
```

## Open achievements

### Via the Overlay object

```csharp
SteamSettings.Client.overlay.OpenAchievements();
```

### Via a User Data object

This assumes you have a [UserData ](../user-data.md)object named `userData` and will open the achievements of this user's entry if available to the user making the call e.g. if this user is a friend.

```csharp
userData.OpenAchievements();
```

## Open player chat

### Via the Overlay object

```csharp
SteamSettings.Client.overlay.OpenChat(userId);
```

### Via a User Data object

This assumes you have a [UserData ](../user-data.md)object named `userData`

```csharp
userData.OpenChat();
```

Note you can send a chat message without opening the overlay via&#x20;

```csharp
userData.SendMessage("message to send");
```

You can also listen for friend chat messages in game e.g. you can receive and display friend chat messages in game without opening the overlay.

```csharp
SteamSettings.Client.ListenForFriendMessages( true or false );
```

Once done the `evtRecievedFriendChatMessage` event will be invoked when any message is received from any friend, so you should handle that message in your UI code such as&#x20;

```csharp
...
private void Start()
{
    SteamSettings.Client.evtRecievedFriendChatMessage.AddListener(
        HandleChatMessageReceived);
}
...
private void HandleChatMessageRecieved(
    UserData sender, 
    string message, 
    EChatEntryType type)
{
    if(type == EChatEntryType.k_EChatEntryTypeChatMsg)
    {
        //This is a regular chat message so show it in a chat UI
    }
}
```

## Open add friend

### Via the Overlay object

```csharp
SteamSettings.Client.overlay.OpenFriendAdd(friendId);
```

### Via a User Data object

This assumes you have a [UserData ](../user-data.md)object named `userData`

```csharp
userData.OpenFriendAdd();
```

## Open remove friend

### Via the Overlay object

```csharp
SteamSettings.Client.overlay.OpenFriendRemove(friendId);
```

### Via a User Data object

This assumes you have a [UserData ](../user-data.md)object named `userData`

```csharp
userData.OpenFriendRemove();
```
