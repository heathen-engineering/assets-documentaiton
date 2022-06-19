# User.Client

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction

```csharp
using UserApi = HeathenEngineering.SteamworksIntegration.API.User.Client;
```

```csharp
public static class User.Client
```

### What can it do?

The user interface can be used to modify the local user's rich presence data and read data from other users. In large the features and capabilities of the User interface are available through the related data object

### Related Obejct

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/user-data" %}

## How To

### Get the local user

{% hint style="info" %}
The simplest way is&#x20;

```csharp
var myData = UserData.Me;
```
{% endhint %}

You can read this from the API as well

```csharp
var user = API.User.Client.Id;
```

you can also get key data about the local user either from the resulting [User Data](../objects/user-data.md) object as read from ID or directly from the interface as shown below

```csharp
var userLevel = API.User.Client.Level;
```

```csharp
var richData = API.User.Client.RichPresence;
```

```csharp
var level = API.User.Client.GetGameBadgeLevel(series, foil);
```

### Get and set rich data

Set the rich presence data for an unsecured game server that the user is playing on. This allows friends to be able to view the game info and join your game.

```csharp
API.User.Client.AdvertiseGame(serverId, ip, port);
```

```csharp
API.User.Client.SetRichPresence(key, value);
```

```csharp
API.User.Client.ClearRichPresence();
```

```csharp
API.User.Client.GetRichPresence(key);
```

### Duration Control

Heathen engineering is not and will never support this sort of behaviour. If you need it look else where.

The  same applies for SetDurationControlOnlineState and anything of similar nature.
