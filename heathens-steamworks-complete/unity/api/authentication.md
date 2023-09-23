---
description: Access the Steam authentication system with Heathen's Steam API
---

# Authentication

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using API = HeathenEngineering.SteamworksIntegration.API;
```

```csharp
public static class API.Authentication
```

{% hint style="success" %}
The Authentication API will use the Server or Client version of Valve's Steam API as required. It is not separated into a .Client or .Server version like other APIs as all features are exactly the same between them.
{% endhint %}

The Authentication has both client and server interfaces that are identical. Heathen's Steam API wrap's these in a single call which will call the appropriate client or server interface for you based on the build type in Unity.

### What can it do?

The Authentication interface can be used to generate and validate session tickets. This is most commonly used with Steam Game Server but can also be used to for inventory verification or other similar verified processes.

### Related Objects

{% embed url="https://kb.heathen.group/assets/steamworks/objects/authentication-session" %}

{% embed url="https://kb.heathen.group/assets/steamworks/objects/authentication-ticket" %}

## Fields and Attributes

### Active Tickets

[Tickets](../objects/authentication-ticket.md) this player has sent out.

```csharp
public static List<AuthenticationTicket> ActiveTickets;
```

### Active Sessions

[Sessions](../objects/authentication-session.md) the player has started.

```csharp
public static List<AuthenticationSession> ActiveSessions;
```

## Methods

### IsAuthTicketValid

```csharp
public static bool IsAuthTicketValid(AuthenticationTicket ticket);
```

Determines if the provided ticket handle is valid

### EncodedAuthTicket

```csharp
public static string EncodedAuthTicket(AuthenticationTicket ticket);
```

Encodes a ticket to hex string format

This is most commonly used with web calls such as [https://partner.steamgames.com/doc/webapi/ISteamUserAuth#AuthenticateUserTicket](https://partner.steamgames.com/doc/webapi/ISteamUserAuth#AuthenticateUserTicket)

### GetAuthSessionTicket

```csharp
//Ticket for a Steam User or Steam Game Server
public static void GetAuthSessionTicket(CSteamID identity,
        Action<AuthenticationTicket, bool> callback);
```

```csharp
//Native use of Steam Networking Identity
public static void GetAuthSessionTicket(SteamNetworkingIdentity identity,
        Action<AuthenticationTicket, bool> callback);
```

```csharp
//Ticket for Steam Web API use
public static void GetAuthSessionTicket(string identity,
        Action<AuthenticationTicket, bool> callback);
```

{% hint style="info" %}
The callback delegate should be in the form of

```csharp
void CallbackHandler(AuthenticationTicket result, bool IOError);
```
{% endhint %}

Requests a new Auth Session Ticket

### CancelAuthTicket

```csharp
public static void CancelAuthTicket(AuthenticationTicket ticket);
```

Cancels the auth ticket rather its client or server based.

### BeginAuthSession

```csharp
public static EBeginAuthSessionResult BeginAuthSession(byte[] authTicket, 
                                CSteamID user, 
                                Action<AuthenticationSession> callback);
```

{% hint style="info" %}
The callback deligate should be in the form of

```csharp
void CallbackHandler(AuthenticationSession result);
```
{% endhint %}

Starts an authorization session with the indicated user given the applied auth ticket

### EndAuthSession

```csharp
public static void EndAuthSession(CSteamID user);
```

Ends the auth session with the indicated user if any

### UserHasLicenseForApp

```csharp
public static EUserHasLicenseForAppResult UserHasLicenseForApp(CSteamID user,
                                                                AppId_t appId);
```

Checks if the user owns a specific piece of Downloadable Content (DLC).

### EndAllSessions

```csharp
public static void EndAllSessions();
```

Ends all tracked sessions

### CancelAllTickets

```csharp
public static void CancelAllTickets();
```

Cancels all tracked tickets

## How To

### Get a new ticket

To authenticate the user who needs to be authenticated will first get a ticket and then send that data to the entity that will be doing the authentication ... so typically a client gets a ticket and sends it to a server.

```csharp
API.Authentication.GetAuthSessionTicket(targetSteamId, (result, IOError) =>
{
    if(!IOError)
    {
        //result.Data is your ticket data, use it well
    }
});
```

The act of sending your ticket data to your server or the other client that wishes to authenticate you is up to your networking solution. Rather that is Mirror, MLAPI, Forge, etc. you will need to send the ticket.Data to that user.

#### Target Steam ID

Valve added a new parameter to the Get Authentication Ticket process where its necessary to identify who the ticket is intended for. The targetSteamId parameter is simply that the Steam ID of the user or Steam Game Server that will be using the ticket.

### Begin a session

When ticket data is recieved you need to begin the auth session with that user and confirm the status of that session.

```csharp
var result = API.Authentication.BeginAuthSession(ticket, user, (responce) =>
{
    // responce is an AuthenticationSession
    // You can use this value to understand the state of the session
});

if(result != EBeginAuthSessionResult.k_EBeginAuthSessionResultOK)
{
    // The ticket is not valid,
    // result is and enum of type EBeginAuthSessionResult
    // its value indicates what is wrong
}
```

You can find details on the possible values for the EBeginAuthSessionResult result here:

{% embed url="https://partner.steamgames.com/doc/api/steam_api#EBeginAuthSessionResult" %}

### Ending it

Rather from the authenticated user or the authenticating system a session should be ended when its no longer needed.

To cancel a ticket you sent out

```csharp
API.Authentication.CencelAuthTicket(ticket);
```

To cancel all tickets you sent out

```csharp
API.Authentication.CancelAllTickets();
```

To end a session you started

```csharp
API.Authentication.EndAuthSession(user);
```

To end all sessions you started

```csharp
API.Authentication.EndAllSessions();
```

### Review open tickets and sessions

Your systems should maintain track of its tickets and sessions however the Authenticaitton API does keep a record of all active sessions and tickets.

{% hint style="warning" %}
Do not add or remove tickets or sessions manually
{% endhint %}

the API.Authentication.ActiveTickets and API.Authenticaiton.ActiveSessions lists can be used to iterate over the active tickets and sessions as required.
