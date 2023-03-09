---
description: Configurating your Steam Game Server settings
---

# Configuration

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../">Guides and Tutorials</a></td><td><a href="../../../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../">..</a></td><td><a href="../../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../../../assets/physkit/">physkit</a></td><td><a href="../../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../../../assets/ux/">ux</a></td><td><a href="../../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% hint style="info" %}
Note for a server to be listed properly in the Steam Game Server Browser you must set the server name.
{% endhint %}

<figure><img src="../../../../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Screen shot of a Heathen Steam Settings object with the Game Server config expanded</p></figcaption></figure>

If your working in C# and not using scriptable objects at all you can create a [SteamGameServerConfiguraiton ](../../../../../../assets/steamworks/objects/steam-game-server-configuration.md)and pass that to the [API.App.Server.Initialization(...)](../../../../../../assets/steamworks/api/app.server.md#initialize) method.

## Raw API

Heathen's API is a direct wrapper of the raw Steam API so there is no black magic to worry about. You can review our code for initialization in the `API.App.cs` file. The following notes might help thouse looking to work with the raw API.

### Values

You must set your configuration values before you call Log On and after Initialization.

```csharp
var Initialized = GameServer.Init(serverConfiguration.ip, 
                                  serverConfiguration.gamePort, 
                                  serverConfiguration.queryPort, 
                                  eMode, 
                                  serverConfiguration.serverVersion);
                                         
//...
if(Initialized)
{
   SteamGameServer.SetModDir(serverConfiguration.gameDirectory);
   SteamGameServer.SetProduct(appId.ToString());
   SteamGameServer.SetGameDescription(serverConfiguration.gameDescription);
   SteamGameServer.SetMaxPlayerCount(serverConfiguration.maxPlayerCount);
   SteamGameServer.SetPasswordProtected(serverConfiguration.isPasswordProtected);
   SteamGameServer.SetServerName(serverConfiguration.serverName);
   SteamGameServer.SetBotPlayerCount(serverConfiguration.botPlayerCount);
   SteamGameServer.SetMapName(serverConfiguration.mapName);
   SteamGameServer.SetDedicatedServer(serverConfiguration.isDedicated);

   //...

   SteamGameServer.LogOnAnonymous();
   // or NOT BOTH
   SteamGameServer.LogOn(Configuration.gameServerToken);
}

```

The one exception to this rule is the `SteamGameServer.SetAdvertiseServerActive(true);` which can be set after logon and toggled on and off as required.

{% hint style="info" %}
`SteamGameServer.SetAdvertiseServerActive(true);`

Is what tells the server to advertise its self on the Steam Game Server Browser system. if this is false it will not be listed, if it lacks a name it will not be listed.
{% endhint %}
