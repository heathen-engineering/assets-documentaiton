---
description: Configurating your Steam Game Server settings
---

# ⚙ Configuration

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
Note For a server to be listed properly in the Steam Game Server Browser you must set the server name.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (4) (2).png" alt=""><figcaption><p>Screen shot of a Heathen Steam Settings object with the Game Server config expanded</p></figcaption></figure>

If you're working in C# and not using scriptable objects at all you can create a [SteamGameServerConfiguraiton ](../../../../../assets/steamworks/unity-engine/objects/steam-game-server-configuration.md)and pass that to the [API.App.Server.Initialization(...)](../../../../../assets/steamworks/unity-engine/api/app.server.md#initialize) method.

## Raw API

Heathen's API is a direct wrapper of the raw Steam API so there is no black magic to worry about. You can review our code for initialization in the `API.App.cs` file. The following notes might help those looking to work with the raw API.

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

The one exception to this rule is that `SteamGameServer.SetAdvertiseServerActive(true);` which can be set after login and toggled on and off as required.

{% hint style="info" %}
`SteamGameServer.SetAdvertiseServerActive(true);`

This is what tells the server to advertise itself on the Steam Game Server Browser system. if this is false it will not be listed, if it lacks a name it will not be listed.
{% endhint %}
