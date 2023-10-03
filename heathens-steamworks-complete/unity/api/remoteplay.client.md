---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# RemotePlay.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using RemotePlay = HeathenEngineering.SteamworksIntegration.API.RemotePlay.Client;
```

```csharp
public static class RemotePlay.Client
```

### What can it do?

Functions that provide information about Steam Remote Play sessions, streaming your game content to another computer or to a Steam Link app or hardware.

## Events

### Session Connected

Called when a session connects

```csharp
public static SteamRemotePlaySessionConnectedEvent EventSessionConnected;
```

The handler would take the form

```csharp
void Handler(SteamRemotePlaySessionConnected_t responce)
{
    //Do Work
}
```

### Session Disconnected

Called when a session disconnects

```csharp
public static SteamRemotePlaySessionDisconnectedEvent EventSessionDisconnected;
```

The handler would take the form

```csharp
void Handler(SteamRemotePlaySessionDisconnected_t responce)
{
    //Do Work
}
```

## How To

### Get Session Counts

Get the number of currently connected sessions

```csharp
var count = API.RemotePlay.Client.GetSessionCounts();
```

### Get Sessions

Get the collection of current remote play sessions

```csharp
var sessions = API.RemotePlay.Client.GetSessions();
```

### Get Session User

Gets the user data of the connected session user

```csharp
var user = API.RemotePlay.Client.GetSessionUser(session);
```

### Get Session Client Name

Gets the name of the session client device

```csharp
var name = API.RemotePlay.Client.GetSessionClientName(session);
```

### Get Session Client Formfactor

Gets the formfactor of the connected session

```csharp
var formfactor = API.RemotePlay.Client.GetSessionClientFormFactor(session);
```

### Get Session Client Resolution

Get the resolution of the connected session

```csharp
var resolution = API.RemotePlay.Client.GetSessionClientResolution(session);
```

### Send Invite

Invite a friend to join the game using remote play together

```csharp
if(API.RemotePlayClient.SendInvite(user))
    Debug.Log("Done");
else
    Debug.Log("Send failed");
```
