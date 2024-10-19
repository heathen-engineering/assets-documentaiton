---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Steam Game Server Configuration

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Used to define a Game Server's configuration

```csharp
public struct SteamGameServerConfiguration
```

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

each 8 bit segment storing a different octave. We have tools that can convert this to a string or a string based IP to a uint see our [Utilities ](../../api-extensions/utilities.md)for more information.

### IpAdress

The string representation of the IP address

```csharp
public string IpAddress {get; set; }
```

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

### Get

Gets the SteamGameServerConfiguraiton from the target. This can be used to read the configuration from files or to read the configuration applied to the current game.

```csharp
public static SteamGameServerConfiguraiton Get();

public static bool Get(FileInfo configFile, out SteamGameServerConfiguration config);

public static bool Get(string configFile, out SteamGameServerConfiguration config);

public static bool Get(byte[] data, out SteamGameServerConfiguration config);
```

### ToString

Returns the JSON formated string of the configuraiton

```csharp
public string ToString()
```

### ToBytes

Returns the byte\[] representing the configuraiton

```csharp
public byte[] ToBytes()
```

### SaveToDisk

Saves the config to a file on the local disk

```csharp
public bool SaveToDisk(string path)
```
