---
description: Representing a Steam Clan aka Steam Group
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Clan Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using HeathenEngineering.SteamworksIntegration;
```

```csharp
public struct ClanData : IEquatable<CSteamID>, 
                         IEquatable<ClanData>, 
                         IEquatable<ulong>, 
                         IComparable<CSteamID>, 
                         IComparable<ClanData>, 
                         IComparable<ulong>
```

The clan structure is used by most of the features of the API.Clans interface. Its returned by GetClans and similar methods and is an input for most methods.

The Clan structure is interchangable with CSteamID and ulong

```csharp
ClanData clan = new CSteamID(id);
CSteamID clanId = clan;
ulong clanIdValue = clan;
Clan clanCopy = clanIdValue;
```

{% hint style="success" %}
Valve did a big update to Group chat and Friend chat and in so doing broke a very cool feature in "Clan Chat".\
\
You can still use Clan Chat but it is not the same chat that you see in the Steam client. there is at current no way to use the Steam client Friend chat features in the Steam API. \
\
If you use Clan Chat it will only work for users that join and chat through the Steam API not the user's who are using the Steam Client's Friend Chat feature.\
\
Note you can and probably should forgo using Clan chat in game and instead simply open the overlay to the friend chat when needed.\
\
We keep this present as in some cases it can be used as a "game" global chat, by joining the player to the game's offical "clan" aka "group" and showing that in game. Just remimber this will only be relevant for the players currently in game and is not the same as the chat seen in the Steam Client / Overlay
{% endhint %}

## Fields and Attributes

### SteamId

```csharp
public CSteamID SteamId { get; set; }
```

The Steam API native CSteamID value for this&#x20;

### AccountId

```csharp
public AccountID_t { get; set; }
```

The account ID segment of the full CSteamID, to understand more read [this article](../../../steam/csteamid.md).

### FriendId

```csharp
public uint FriendId { get; set; }
```

The underlying uint value of the AccountID\_t segment of the CSteamID, to understand more read [this article](../../../steam/csteamid.md).

### IsValid

```csharp
public bool IsValid => get;
```

This indicates rather or not the underlying CSteamID is of the proper Universe and Type it does not indicate that it is a valid entry. E.g. this tells you if the data is of the right shape ... not that it equates to a valid entry in Steam client.

### Icon

```csharp
public Texture2D Icon => get;
```

Returns the loaded texture if any,&#x20;

{% hint style="info" %}
This will be null if you have not yet loaded this icon. Call the method LoadIcon to load the icon. Note you really shouldn't need to use this in most cases, simply calling LoadIcon is faster and safer. This is only really useful to see if the icon had already been loaded e.g. if this is null then no.
{% endhint %}

### Name

```csharp
public string Name => get;
```

Returns the display name of this clan localized to the local user if available.

### Tag

```csharp
public string Tag => get; 
```

Returns the clan tag for this clan

### Owner

```csharp
public UserData Owner => get;
```

Returns the Steam user that owns this clan

### Officers

```csharp
public UserData[] Officers => get;
```

Returns a collection of the officers of this clan if visible to the user.

### Number Of Members In Chat

```csharp
public int NumberOfMembersInChat => get;
```

Returns the number of members in the chat, note for large chats Steam may not be able to fully iterate the members so for big clans consider this a :man\_shrugging:

### Members In Chat

```csharp
public UserData[] MembersInChat => get;
```

As much as Steam API is able to do so this will produce a collection of the user's in the chat.&#x20;

{% hint style="info" %}
Valve notes in its own documentation that very large clans cannot be iterated properly so this may be a partial or empty list.
{% endhint %}

### Is Official Game Group

```csharp
public bool IsOfficalGameGroup => get;
```

True if this clan is a game's official group / clan as opposed to being a user's clan / group. Note every game has an official "group" this is represented on Steam's backend as a "Clan" and includes chats, forums and other social network features.

### Is Public

```csharp
public bool IsPublic => get;
```

Is this clan a public clan or a private clan

### Is User Owner

```csharp
public bool IsUserOwner => get;
```

Is the local user the owner of this clan

### Is User Officer

```csharp
public bool IsUserOfficer => get;
```

Is the local user an officer of this clan, note this iterates the officers, its generally better to do this your self such as&#x20;

```csharp
var officers = clan.Officers;
if(officers.Any(p => p == UserData.Me))
{
    //Yes the user is an officer
}
else
{
    //No the user is not an officer ... or there are to many officers to properly iterate
}
```



## Methods

### Get

A set of static method for fetching the ClanData object based on various forms of the ID or to get a list of all clans the user is a member of

```csharp
//Get all clans the user is a member of
public static ClanData[] Get();

//Get a clan by id info
public static ClanData Get(uint accountId)
public static ClanData Get(AccountID_t accountId)
public static ClanData Get(ulong id)
public static ClanData Get(CSteamID id)
```

### Join Chat

```csharp
public void JoinChat(Action<ClanChatRoom, bool> callback);
```

The JoinChat method will attempt to join the user to clan's chat room. The resulting callback will return a ClanChatRoom object indicating the state, providing access to the chat and being of use in other chat related methods.

### Load Icon

```csharp
public void LoadIcon(Action<Texture2D> callback)
```

Loads the icon if not already loaded, returns the icon once loaded
