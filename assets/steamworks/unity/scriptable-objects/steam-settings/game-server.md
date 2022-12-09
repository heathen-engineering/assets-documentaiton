# Game Server

<figure><img src="../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

accessed from within the SteamSettings this houses server specific features and functions

## Definition

```csharp
public class SteamSettings : ScriptableObject
{
    public class GameServer;
}
```

A static accessor is available that will access the active server object

```csharp
SteamSettings.Server
```

## Events

### disconnected

occurs when the server disconnects from Steam

### connected

occurs when the server connects to Steam

### failure

occurs when an error occurs as reported by Steam

## Fields and Attributes

### autoInitalize

```csharp
bool autoInitalize;
```

Indicates rather or not the Server APIs should auto initialize on start up

### autoLogon

```csharp
bool autoLogon;
```

indicates rather or not the Steam Game Server system should log on after initialization

### ip

```csharp
uint ip;
```

The uint packed IP address, this is the raw form Steam would use IP address as and is simply the 4 octives of an IP address packed into the 32 bit int value

&#x20;`00000000 00000000 00000000 00000000`&#x20;

each 8 bit segment storing a different octave. We have tools that can convert this to a string or a string based IP to a uint see our [Utilities ](../../../api/utilities.md)for more information.

### queryPort

```csharp
ushort queryPort;
```

The query port used by Valve

### gamePort

```csharp
ushort queryPort;
```

The query port used by Valve

### serverVersion

```csharp
string serverVersion;
```

The server version to report to Steam Game Server&#x20;

### serverId

```csharp
CSteamID serverId;
```

The ID assigned to the Steam Game Server on initialization and logon. This is set by Steam and is what you would as an address to connect to this server

### usingGameServerAuthApi

```csharp
bool usingGameServerAuthApi;
```

Should the auth API be used

### enableHeartbeats

```csharp
bool enableHeartbeats;
```

Should we send heartbeats to SGS, if you do not do this then the Steam Game Server Browser will not be able to update ping and other bits of data.

### spectatorServerName

```csharp
bool spectatorServerName;
```

The name of the server to display in the spectator list

### anonymousServerLogin

```csharp
bool anonymousServerLogin;
```

{% hint style="success" %}
Recommended (set this to true)
{% endhint %}

Should the interface logon anonymously

### gameServerToken

```csharp
string gameServerToken;
```

if not logging on anonymously then it must have a token [https://steamcommunity.com/dev/managegameservers](https://steamcommunity.com/dev/managegameservers)

### isPasswordProtected

```csharp
bool isPasswordProtected;
```

Indicate to SGS that this server is password protected, its up to you to set that password and handle its use this only lets the browser know one is required.

### gameName

```csharp
string gameName;
```

The name to display for the server in the SGS browser

### gameDescription

```csharp
string gameDescription;
```

The description to display for the server in SGS browser

### gameDirectory

```csharp
string gameDirectory;
```

the name of the folder in Steam content the game is running from. Usually the same as the game's name.

### isDedicated

```csharp
bool isDedicated;
```

Indicate to SGS browser this server is dedicated

### maxPlayerCount

```csharp
int maxPlayerCount;
```

Indicate to SGS what the max player count is

### botPlayerCount

```csharp
int botPlayerCount;
```

Indicate to SGS what the bot player count is

### mapName

```csharp
string mapName;
```

reports the map name to SGS

### gameData

```csharp
string gameData;
```

Delimited string used for matchmaking filtering

### rulePairs

```csharp
List<StringKeyValuePair> rulePairs;
```

The set of rule pairs for the server

## Methods

### Init

```csharp
public void Init();
```

Used internally to initialize the server APIs

### LogOn

```csharp
public void LogOn();
```

Used to log the server on, typically this will be called automatically assuming you have set autoLogon to true.
