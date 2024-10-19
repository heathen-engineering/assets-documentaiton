---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Authentication Session

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

<pre class="language-csharp"><code class="lang-csharp"><strong>using HeathenEngineering.SteamworksIntegration;
</strong></code></pre>

```csharp
public class AuthenticationSession
```

Used by the [Authentication ](../../api-extensions/authentication.md)interface to represent an active authentication session

## Events

### OnStartCallback

```csharp
public Action<AuthenticationSession> OnStartCallback;
```

A delegate to be called when the authentication session response is returned by Valve.

## Fields and Attributes

### IsClientSession

```csharp
public bool IsClientSession => get;
```

Is this session object related to a client or server session, this is generally only relevant internally to Heathen's tools.

### User

```csharp
public UserData User => get;
```

The user this session is related to

### GameOwner

```csharp
public UserData GameOwner => get;
```

The user that owns the game, is generally the same as User, if it is not it means the User is borrowing the game such as via Family Sharing.

### Data

```csharp
byte[] Data => get;
```

The session data, aka the ticket itself

### Response

```csharp
public EAuthSessionResponse Response => get;
```

The response received when validating a provided ticket.

### IsBarrowed

```csharp
public bool IsBarrowed => get;
```

Indicates the owner and user are not the same.

## Methods

### Constructor

```csharp
public AuthenticationSession(CSteamID userId, 
                             Action<AuthenticationSession> callback, 
                             bool isClient = true)
```

* userId\
  This is the anticipated user that this session is for
* callback\
  This is a delegate to be invoked when the session response is available
* isClient\
  is this a client session or server session, in P2P its always a client session.

### End

```csharp
public void End();
```

Ends this session&#x20;
