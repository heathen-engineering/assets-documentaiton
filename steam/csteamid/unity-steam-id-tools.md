---
cover: ../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Unity Steam ID tools

## Introduction

Steam IDs are used for a lot of different things and each has its own set of features and functions. For example, a CSteamID can represent a user and users have additional features like name, nickname, rich presence, etc. Alternatively, a CSteamID could represent a lobby which has features like metadata, members, etc.

Heathen has created a set of wrappers that let you treat each ID as a unique type and simplify working with the features of each unique type. Note each of these is implicitly convertible ... that is you can use them as if they are CSteamID\_t or ulong and you can assign them from CSteamID\_t or ulong. These also have additional handlers to help you work with them as AccountID\_t

### [Clan](../../heathens-steamworks-complete/unity/data-layer/clan-data.md)

This is for IDs that represent a "clan" or "group"

### [Lobby](../../heathens-steamworks-complete/unity/data-layer/lobby-data.md)

This is for IDs that represent lobbies aka chats

### [UserData](../../heathens-steamworks-complete/unity/data-layer/user-data.md)

This is for IDs that represent users

## Creating Steam Ids

While the full CSteamID is a 64-bit long ... not very human-friendly number the actual "unique" part is just 32-bits long and much more manageable by a human. If you know the "type" of the ID then you can reconstruct it providing only the 32-bit "account Id" part.

### Examples

#### Adding Friends

Let's say you want your users to be able to "invite" each other to become friends through some method outside of Steam such as chat, stream, etc. You could simply show the user their "Friend ID" aka the Account ID of their CSteamID. They can provide this fairly short number to prospective friends.

To display the local user's Friend ID we can simply read it from the local user's User Data.

```csharp
textField.text = UserData.Me.FriendId.ToString();
```

This will populate a simple number in the provided text field.

You can then also provide an inputField where users can type in the IDs they get from others. The friend ID typed in can then be used to construct a UserData object which you can use for anything you like including Adding to Friends.

```csharp
//Parse the input string to a uint value
uint FriendID = System.Convert.ToUint32(inputfield.text);
//Get the UserData for this friend ID
UserData newGuy = UserData.Get(FriendID);
//Invite this user to be our friend on Steam
API.Overlay.Client.Activate(FriendDialog.friendadd, newGuy);
```

We even have a shortcut you can use to do this all in 1 line

```csharp

if(UserData.AddFriend(inputField.text))
{
    //text was parsed to a uint value and sent to Steam
}
else
{
    //text is not a unit value, and no action was taken
}
```

#### Sharing Lobbies

Let's say you want to share a simple string so that players can join lobbies automatically. You could do this in a few ways but one option is to share the lobbies and one is to expose the lobby's account ID.

```csharp
lobbyIdField.text = myLobby.AccountId;
```

As with the Add Friend example you can then join a lobby via the ID

```csharp
//Parse the input string to a uint value
uint LobbyAccountID = System.Convert.ToUint32(inputfield.text);
//Get the UserData for this friend ID
Lobby newLobby = Lobby.Get(LobbyAccountID );
//Invite this user to be our friend on Steam
mewLobby.Join(CallbackHandler);
```

This can even be done in 1 line

```csharp
if(Lobby.Join(inputfield.text, CallbackHandler))
{
    //input text was parsed and sent to Steam
}
else
{
    //Invalid input text, no action taken
}
```
