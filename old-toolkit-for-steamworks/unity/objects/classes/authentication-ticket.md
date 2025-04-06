---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Authentication Ticket

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using HeathenEngineering.SteamworksIntegration;
```

```csharp
public class AuthenticationTicket
```

Used by the [Authentication ](../../api-extensions/authentication.md)interface to represent an active authentication ticket

## Events

### Callback

```csharp
public Action<AuthenticationTicket, bool> Callback;
```

A delegate to be invoked when the ticket is ready for use.

Example handler

```csharp
public void EventHandler(AuthenticationTicket result, bool IOError)
{
}
```

## Fields and Attributes

### IsClientTicket

```csharp
public bool IsClientTicket => get;
```

Indicates this ticket is being managed by a client or server

### Handle

```csharp
public HAuthTIcket Handle => get;
```

The authentication handle associated with this ticket

### Data

```csharp
public byte[] Data => get;
```

The ticket data of this ticket is what should be sent to whoever it is that will be calling BeginSession for this ticket.

### Verified

```csharp
public bool Verified => get;
```

Has this ticket been verified, this gets set to true when the Get Authentication Session response comes back from the Valve's backend.

### CreatedOn

```csharp
public uint CreatedOn => get;
```

The Steamworks DateTime this ticket was created ... this is Linux Epoc time e.g. the number of seconds since Jan 1 1970. In general, you do not need to bother with this we use it to calculate the ticket age for you in the Age field.

### Result

```csharp
public EResult Result => get;
```

The result of the ticket

## Methods

### Constructor

```csharp
public AuthenticationTicket(SteamNetworkingIdentity forIdentity, 
                            Action<AuthenticationTicket, bool> callback, 
                            bool isClient = true)
```

The above: constructs a new ticket given a particular identity. The identity should be the User or Game Server that this ticket will be used by. Note that a lobby is not a server.

```csharp
public AuthenticationTicket(byte[] dataToInclude, 
                            Action<AuthenticationTicket, bool> callback)
```

The above: constructs a new ticket given existing ticket data

```csharp
public AuthenticationTicket(string webIdentity, 
                            Action<AuthenticationTicket, bool> callback)
```

The above: constructs a new ticket for a web identity, this string can be empty and is defined by the web service that will be using the ticket.

### Cancel

```csharp
public void Cancel();
```

Cancels this ticket
