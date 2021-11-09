---
description: Access the Steam authentication system with Heathen's Steam API
---

# Authentication

## Introduction

```csharp
public static class API.Authentication
```

The Authenticaiton has both client and server interfaces that are identical. Heathen's Steam API wrapps these in a single call which will call the appropreate client or server interface for you based on the build type in Unity.

### What can it do?

The Authentication interface can be used to generate and validate session tickets. This is most commonly used with Steam Game Server but can also be used to for inventory varification or other similar verified processes.

## How To

### Get a new ticket

To authenticate the user who needs to be authenticated will first get a ticket and then send that data to the entity that will be doing the authentication ... so typically a client gets a ticket and sends it to a server.

```csharp
API.Authentication.GetAuthSessionTicket((result, IOError) =>
{
    if(!IOError)
    {
        //result.Data is your ticket data, use it well
    }
});
```

The act of sending your ticket data to your server or the other client that wishes to authenticate you is up to your networking solution. Rather that is Mirror, MLAPI, Forge, etc. you will need to send the ticket.Data to that user.

### Begin a session

When ticket data is recieved you need to begin the auth session with that user and confirm the status of that session.

```csharp
API.Authentication.BeginAuthSession(ticket, user, (result, IOError) =>
{
    //result is the result and provides information as to the state of teh authenitcaiton.
});
```

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
