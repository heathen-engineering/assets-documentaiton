---
description: Understanding Steam's Unique ID
---

# 🆔 CSteamID

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

CSteamID also known simply as "Steam ID" is a ulong value (64 bits) and is used by Steam API to uniquely identify ... well most things.&#x20;

Heathen has created wrap-around structures like [UserData ](../../heathens-steamworks-complete/unity/data-layer/user-data.md)and [Lobby ](../../heathens-steamworks-complete/unity/data-layer/lobby-data.md)that are interchangeable with CSteamID and ulong and provide helpful features unique to each use case of the ID. In most cases, you should be using [UserData](../../heathens-steamworks-complete/unity/data-layer/user-data.md), [Lobby](../../heathens-steamworks-complete/unity/data-layer/lobby-data.md), [Clan](../../heathens-steamworks-complete/unity/data-layer/clan-data.md), etc. and not need to bother with the raw CSteamID or its ulong value.

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

The data type AccountId\_t is a wrapper around the uint primitive type ... that is it is a uint value with a few extra features.

### Account Instance

```csharp
uint unAccountInstance;
```

This value is readable on the CSteamID but not documented in Steam.&#x20;

We know from reviewing the CSteamID struct and its various methods that for Type Clan and GameServer the account instance is set to&#x20;

```csharp
unAccountInstance = 0u;
```

For all other types, Steam sets the value to&#x20;

```csharp
unAccountInstance = 1u;
```

We know from experience that attempting to set a lobby in this way will fail resulting in an invalid lobby. We have deduced that lobbies (seem) to have a constant account instance value of

```csharp
unAccountInstance = 393216u;
```
