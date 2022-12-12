# RemotePlay.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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
