---
description: Understanding Steam's Unique ID
---

# CSteamID

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

CSteamID also known simply as "Steam ID" is a ulong value (64 bits) and is used by Steam API to uniquely identify ... well most things.&#x20;

Heathen has created wrap around structures like [UserData ](../../objects/user-data.md)and [Lobby ](../../objects/lobby.md)that are interchangeable with CSteamID and ulong and provide helpful features unique to each use case of the ID. In most cases you should be using [UserData](../../objects/user-data.md), [Lobby](../../objects/lobby.md), [Clan](../../objects/clan.md), etc. and not needing to bother with the raw CSteamID or its ulong value.

The native CSteamID ulong value is composed of 4 main parts

### Universe

```csharp
namespace Steamworks
{
    public enum EUniverse
    {
        k_EUniverseInvalid = 0,
        k_EUniversePublic = 1,
        k_EUniverseBeta = 2,
        k_EUniverseInternal = 3,
        k_EUniverseDev = 4,
        k_EUniverseMax = 5
    }
}
```

### Type

```csharp
namespace Steamworks
{
    public enum EAccountType
    {
        k_EAccountTypeInvalid = 0,
        k_EAccountTypeIndividual = 1,
        k_EAccountTypeMultiseat = 2,
        k_EAccountTypeGameServer = 3,
        k_EAccountTypeAnonGameServer = 4,
        k_EAccountTypePending = 5,
        k_EAccountTypeContentServer = 6,
        k_EAccountTypeClan = 7,
        k_EAccountTypeChat = 8,
        k_EAccountTypeConsoleUser = 9,
        k_EAccountTypeAnonUser = 10,
        k_EAccountTypeMax = 11
    }
}
```

### Account Id

```csharp
AccountId_t accountId;
```

The data type AccountId\_t is a wrapper around the uint primitive type ... that is it is really a uint value with a few extra features.

### Account Instance

```csharp
uint unAccountInstance;
```

This value is readable on the CSteamID but not documented in Steam.&#x20;

We know from reviewing the CSteamID struct and its various methods that for Type Clan and GameServer the account instance is set to&#x20;

```csharp
unAccountInstance = 0u;
```

For all other types Steam sets the value to&#x20;

```csharp
unAccountInstance = 1u;
```

We know from experience that attempting to set a lobby in this way will fail resulting in an invalid lobby. We have deduced that lobbies (seem) to have a constant account instance value of

```csharp
unAccountInstance = 393216u;
```

## Wrappers

As noted Steam IDs are used for a lot of different things and each has its own set of features and functions. For example a CSteamID can represent a user and users have additional features like name, nickname, rich presence, etc. Alternatively a CSteamID could represent a lobby which has its own features like metadata, members, etc.

Heathen has created a set of wrappers that let you treat each ID as a unique type and simplify working with the features of each unique type. Note each of these are implicitly convertible ... that is you can use them as if they are CSteamID\_t or ulong and you can assign them from CSteamID\_t or ulong. These also have additional handlers to help you work with them as AccountID\_t

### [Clan](../../objects/clan.md)

This is for IDs that represent a "clan" or "group"

### [Lobby](../../objects/lobby.md)

This is for IDs that represent lobbies aka chats

### [UserData](../../objects/user-data.md)

This is for IDs that represent users

## Creating Steam Ids

While the full CSteamID is a 64bit long ... not very human friendly number the actual "unique" part is just 32bits long and much more manageable by a human. If you know the "type" of the ID then you can reconstruct it providing only the 32bit "account Id" part.

### Examples

#### Adding Friends

Lets say you want your user's to be able to "invite" each other to become friends through some method out side of Steam such as chat, stream, etc. You could simply show the user their "Friend ID" aka the Account ID of their CSteamID. They can this provide this fairly short number to prospective friends.

To display the local user's Friend ID we can simply read it from the local user's User Data.

```csharp
textField.text = UserData.Me.FriendId.ToString();
```

This will populate a simple number in the provided text field.

You can then also provide an inputField where user's can type in the IDs they get from others. The friend ID typed in can then be used to construct a UserData object which you can use for anything you like including Adding to Friends.

```csharp
//Parse the input string to a uint value
uint FriendID = System.Convert.ToUint32(inputfield.text);
//Get the UserData for this friend ID
UserData newGuy = UserData.Get(FriendID);
//Invite this user to be our friend in Steam
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
    //text is not a unit value, no action taken
}
```

#### Sharing Lobbies

Lets say you want to share a simple string so that players can join lobbies automatically. You could do this in a few ways but one option is to share the lobbies but one is to expose the lobby's account ID.

```csharp
lobbyIdField.text = myLobby.AccountId;
```

As with the Add Friend example you can then join a lobby via the ID

```csharp
//Parse the input string to a uint value
uint LobbyAccountID = System.Convert.ToUint32(inputfield.text);
//Get the UserData for this friend ID
Lobby newLobby = Lobby.Get(LobbyAccountID );
//Invite this user to be our friend in Steam
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
