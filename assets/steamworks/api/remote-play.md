# Remote Play

## Introduction

```csharp
using API = HeathenEngineering.SteamworksIntegraiton.API;
```

```csharp
public static class API.RemotePlay
```

The whole of the remote play system is only accessible from the Client API as a result you will always be using the form:

```csharp
API.RemotePlay.Client
```

### What can it do?

Functions that provide information about Steam Remote Play sessions, streaming your game content to another computer or to a Steam Link app or hardware.

## Events

### Session Connected

Called when a session connects

### Session Disconnected

Called when a session disconnects

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
