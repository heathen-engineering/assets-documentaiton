---
description: Representing a Steam Clan aka Steam Group
---

# Clan

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct Clan
```

The clan structure is used by most of the features of the API.Clans interface. Its returned by GetClans and similar methods and is an input for most methods.

The Clan structure is interchangable with CSteamID and ulong

```csharp
Clan clan = new CSteamID(id);
CSteamID clanId = clan;
ulong clanIdValue = clan;
Clan clanCopy = clanIdValue;
```

## Fields and Attributes

### ID

```csharp
public CSteamID id;
```

The underlying native ID for this clan

### SteamId

```csharp
public ulong SteamId { get; set; }
```

The underlying ulong value of the CSteamID&#x20;

### AccountId

```csharp
public AccountID_t { get; set; }
```

The account ID segment of the full CSteamID, to understand more read [this article](../unity/quick-start-guide/csteamid.md).

### FriendId

```csharp
public uint FriendId { get; set; }
```

The underlying uint value of the AccountID\_t segment of the CSteamID, to understand more read [this article](../unity/quick-start-guide/csteamid.md).

### IsValid

```csharp
public bool IsValid => get;
```

This indicates rather or not the underlying CSteamID is of the proper Universe and Type it does not indicate that it is a valid entry. E.g. this tells you if the data is of the right shape ... not that it equates to a valid entry in Steam client.



| Type        | Name     | Comment                                  |
| ----------- | -------- | ---------------------------------------- |
| CSteamID    | id       | The CSteamID of the clan                 |
| string      | Name     | Returns the name of the clan             |
| string      | Tag      | Returns the tag of the clan              |
| UserData    | Owner    | Returns the owner of the clan            |
| UserData\[] | Officers | Returns the list of officers of the clan |

## Methods

### Join Chat

```csharp
public void JoinChat(Action<ClanChatRoom, bool> callback);
```

The JoinChat method will attempt to join the user to clan's chat room. The resulting callback will return a ClanChatRoom object indicating the state, providing access to the chat and being of use in other chat related methods.
