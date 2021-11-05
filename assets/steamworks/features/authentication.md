---
description: >-
  Understanding Steam Authentication, when and why to use it ... and when and
  why not to.
---

# Authentication

## Introduction

{% embed url="https://partner.steamgames.com/doc/features/auth" %}

{% hint style="info" %}
The above link and repeated below so you can find it:\
[https://partner.steamgames.com/doc/features/auth](https://partner.steamgames.com/doc/features/auth)\
\
Is highly important, you should fully read Valve's own documentation around Steam Authentication to fully understand it. Some of the information will be summarized here in and notes on the tools and systems Heathen has created around Steam Authentication is documented below.&#x20;
{% endhint %}

### Session Tickets

The relivent aspect of Steam's Authentication for your Unity project are Session Tickets.

> #### [Valve](https://partner.steamgames.com/doc/features/auth)
>
> &#x20;Session Tickets are signed tickets that can be used to verify a user's identity between the user's game client and any number of other game clients (such as in a peer-to-peer multiplayer session) or to a listen/dedicated game server. These tickets can also be used to verify ownership of the current game and related downloadable content, and determine if the user has been VAC-banned (See [Valve Anti-Cheat (VAC) and Game Bans](https://partner.steamgames.com/doc/features/anticheat)).\
> Session Tickets can also be used to verify a user's identity between a game client and a secure, backend server using the [Steamworks Web API](https://partner.steamgames.com/doc/webapi\_overview).&#x20;

## Authenticaiton

Heathen has implamented all of the relvent functionality of the session ticket system in a single static class `Authentication` . This object can be used by client or server to create and validate tickets. The Authenitcaiton class will manage a collection of active tickets and can be used to clean up all active tickets and sessions.

### Members

#### Active Tickets

A collection of the tickets this system has generated.

#### Active Sessions

A collection of the sessions this system has started e.g. tickets it has validated into sessions.

## Ticket

Heathen wraps the Valve ticket data and related information in a helper class named `Ticket` this object can be used to get important information about a ticket such as its age and to cancel the ticket when your done using it.

### Members

#### Is Client Ticket

Indicates that this is or is not a client ticket

#### Handle

The HAuthTicket handle used by Steam processes

#### Data

The byte\[] representing the signed ticket data. This is what should be sent to other clients or servers in order for them to validate this ticket.

#### Verified

This is set to true when Valve responds with the ticket data. When requesting a ticket you should wait till this is true before sending the ticket data on to others for validation.

#### Created On

A linux style date stamp used by Valve processes

#### Age

A TimeSpan representing the age of the ticket

## Session

Heathen wraps the concept of a session as a class object managed by the Authenticaiton class. The Session object will identify key information about an authenticaiton session such as;

### Members

#### Is Client Session

Indicates that this is or is not a client session

#### User

The CSteamID of the user the session relates to

#### Game Owner

The owner of the app the session relates to ... this is usually the same as User however it is possible in Steam's client to barrow games through sharing in which case this is the ID of the user that owns the license to the game while User represents the person playing it and user is the one who is authenticated by the system.

#### Data

A simple byte\[] representing the signed ticket

#### Responce

The last recieved status of the authenticaiton on this session options include

* Ok
* User Not Connect To Steam
* No License Or Expired
* VAC Banned
* Logged In Else Where
* VAC Check Timed Out
* Auth Ticket Canceled
* Auth TIcket Invalid Already Used
* Auth Ticket Invalid
* Publisher Issued Ban

#### Is Barrowed

A bollean which will be true if the User does not match the GameOwner

## Examples

### Get Ticket

To get a ticket that you can later send to other clients or servers for the purpose of authenitcaiton.

{% hint style="info" %}
It is up to you to send the ticket data to the server or client that needs to validate you. This is usually handled by whatever networking tool you are using.
{% endhint %}

#### On a client (non-server build)

```csharp
var ticket = Authentication.ClientGetAuthSessionTicket();
```

#### On a server (server build)

```csharp
var ticket = Authentication.ServerGetAuthSessionTicket();
```

### Send a Ticket

This example will be writen abstracted the specifics of what the command is and how and where it should be called will depend wholly on your chossen networking technology. This example is similar in form and structure to Mirror, MLAPI and others.

```csharp
CmdAuthenticate(ticket.data, SteamUser.GetSteamID());
```

The above assumes the method signature is similar to&#x20;

```csharp
[Command]
public void CmdAuthenticate(byte[] data, CSteamID user);
```

### Begin Session

This is done when you recieve a ticket from someone and wish to validate them starting an authenticaiton session.

{% hint style="warning" %}
You must "end" sessions when you are finished with them e.g. when the user logs off your game server for exmaple.
{% endhint %}

#### On a client (non-server build)

```csharp
Authentication.ClientBeginAuthSession(ticketData, user, (session) =>
{
    if(session.Responce == 0)
    {
        Debug.Log("Authentication Okay for " + session.User.ToString());
    }
});
```

#### On a server (server build)

```csharp
Authentication.ServerBeginAuthSession(ticketData, user,  (session) =>
{
    if(session.Responce == 0)
    {
        Debug.Log("Authentication Okay for " + session.User.ToString());
    }
});
```

Note there is no return on begin auth session rather there is a callback paramiter. The callback has a single paramiter of type Session. [To understand callbacks please read our article on the subject](../../../company/concepts/callbacks.md).

### End Session

{% hint style="warning" %}
You must "end" sessions when you are finished with them e.g. when the user logs off your game server for exmaple.
{% endhint %}

You can end a session in a number of ways

#### With the Session object

```csharp
session.End();

//Remove it from the tracked list if your done with it
Authentication.ActiveSessions.Remove(session);
```

#### With a User ID (client)

```csharp
//Removes any related sessions from the active list
Authentication.ClientEndAuthSession(userId);
```

#### With a User ID (server)

```csharp
//Removes any related sessions from the active list
Authentication.ServerEndAuthSession(userId);
```

#### End All Sessions

```csharp
//Clears the active session list
Authentication.EndAllSessions();
```

### Cancel Ticket

You can cancel any ticket you have created at anytime using one of the following methods. This should generally be done on clean up of the system such as when disconnecting from servers or shutting down.

#### With the Ticket object

```csharp
ticket.Cancel();

//Remove it from the tracked list if your done with it
Authentiication.ActiveTickets.Remove(ticket);
```

#### Cancel All Tickets

```csharp
//This will clear the active tickets list for you
Authenticatiion.CancelAllTickets();
```
