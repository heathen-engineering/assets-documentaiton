# User.Client

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
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

### Related Object

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/user-data" %}

## Fields and Attributes

### IsBehindNAT

```csharp
public static bool IsBehindNAT => get;
```

Checks if the current user looks like they are behind a NAT device.

This is only valid if the user is connected to the Steam servers and may not catch all forms of NAT.

### IsPhoneIdentifying

```csharp
public static bool IsPhoneIdentifying => get;
```

Checks whether the user's phone number is used to uniquely identify them.

### IsPhoneRequiringVerification

```csharp
public static bool IsPhoneRequiringVerification => get;
```

Checks whether the current user's phone number is awaiting (re)verification.

### IsPhoneVerified

```csharp
public static bool IsPhoneVerified => get;
```

Checks whether the current user has verified their phone number.\
\
See the [Steam Guard Mobile Authenticator](https://support.steampowered.com/kb\_article.php?ref=8625-wrah-9030) page on the customer facing Steam Support site for more information.

### IsTwoFactorEnabled

```csharp
public static bool IsTwoFactorEnabled => get;
```

Checks whether the current user has Steam Guard two factor authentication enabled on their account.\
\
See the [Steam Guard Mobile Authenticator](https://support.steampowered.com/kb\_article.php?ref=8625-wrah-9030) page on the customer facing Steam Support site for more information.

### LoggedOn

```csharp
public static bool LoggedOn => get;
```

Checks if the current user's Steam client is connected to the Steam servers.\
\
If it's not then no real-time services provided by the Steamworks API will be enabled. The Steam client will automatically be trying to recreate the connection as often as possible. When the connection is restored a [EventServersConnected](app.md#eventserversconnected) callback will be posted.\
\
You usually don't need to check for this yourself. All of the API calls that rely on this will check internally. Forcefully disabling stuff when the player loses access is usually not a very good experience for the player and you could be preventing them from accessing APIs that do not need a live connection to Steam.

## Methods

### AdvertiseGame

```csharp
public static void AdvertiseGame(CSteamID gameServerId, uint ip, ushort port)
```

```csharp
public static void AdvertiseGame(CSteamID gameServerId, string ip, ushort port)
```

Set the rich presence data for an unsecured game server that the user is playing on. This allows friends to be able to view the game info and join your game.

When you are using Steam authentication system this call is never required, the auth system automatically sets the appropriate rich presence.

### GetGameBadgeLevel

```csharp
public static int GetGameBadgeLevel(int series, bool foil)
```

Gets the level of the users Steam badge for your game.

### RequestStoreAuthURL

```csharp
public static void RequestStoreAuthURL(string redirectUrl, 
                Action<StoreAuthURLResponse_t, bool> callback)
```

Requests a URL which authenticates an in-game browser for store check-out, and then redirects to the specified URL. As long as the in-game browser accepts and handles session cookies, Steam microtransaction checkout pages will automatically recognize the user instead of presenting a login page.

The callback handler should take the form of:

```csharp
void CallbackHandler(StoreAuthURLResponse_t responce, bool IOError)
{
    //Do Work
}
```

You can learn more about the [StoreAuthURLResponse\_t type here.](https://partner.steamgames.com/doc/api/ISteamUser#StoreAuthURLResponse\_t)

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

you can also get key data about the local user either from the resulting [User Data](../data-layer/user-data.md) object as read from ID or directly from the interface as shown below

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
