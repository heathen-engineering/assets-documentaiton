# Game Server

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

accessed from within the SteamSettings this houses server specific features and functions

## Definition

```csharp
public class SteamSettings : ScriptableObject
{
    public class GameClient;
}
```

### Fields and Attributes

| Type                      | Name                   | Comments                                                                                                                                                                             |
| ------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| bool                      | autoInitalize          | indicates rather or not the Server APIs should auto initialize on start up                                                                                                           |
| bool                      | autoLogon              | indicates rather or not the Steam Game Server system should log on after initialization                                                                                              |
| uint                      | ip                     | the uint packed IP address                                                                                                                                                           |
| ushort                    | queryPort              | the query port used by Valve                                                                                                                                                         |
| ushort                    | gamePort               | the game port used by Valve                                                                                                                                                          |
| string                    | serverVersion          | the server version to report to Steam Game Server                                                                                                                                    |
| CSteamID                  | serverId               | <p>the ID assigned to the Steam Game Server on initialization and logon</p><p></p><p>This is set by Steam and is what you would as an address to connect to this server</p>          |
| bool                      | usingGameServerAuthApi | should the auth API be used                                                                                                                                                          |
| bool                      | enableHeartbeats       | should we send heartbeats to SGS                                                                                                                                                     |
| bool                      | spectatorServerName    | the name of the server to display in the spectator list                                                                                                                              |
| bool                      | anonymousServerLogin   | should the interface logon anonymously this is most common                                                                                                                           |
| string                    | gameServerToken        | <p>if not logging on anonymously then it must have a token</p><p><a href="https://steamcommunity.com/dev/managegameservers">https://steamcommunity.com/dev/managegameservers</a></p> |
| bool                      | isPasswordProtected    | indicate to SGS that this server is password protected                                                                                                                               |
| string                    | gameName               | the name to display for the server in the SGS browser                                                                                                                                |
| string                    | gameDescription        | the description to display for the server in SGS browser                                                                                                                             |
| string                    | ganeDirectory          | the name of the folder in Steam content the game is running from                                                                                                                     |
| bool                      | isDedicated            | indicated to SGS browser this server is dedicated                                                                                                                                    |
| int                       | maxPlayerCount         | indicated to SGS what the max player count is                                                                                                                                        |
| int                       | botPlayerCount         | indicated to SGS what the bot player count is                                                                                                                                        |
| string                    | mapName                | reports the map name to SGS                                                                                                                                                          |
| string                    | gameData               | delimited string used for matchmaking filtering                                                                                                                                      |
| List\<StringKeyValuePair> | rulePairs              | the set of rule pairs for the server                                                                                                                                                 |

### Events

#### disconnected

occurs when the server disconnects from Steam

#### connected

occurs when the server connects to Steam

#### failure

occurs when an error occurs as reported by Steam

### Methods

```csharp
public void Init();
```

Used internally to initialize the server APIs

```csharp
public void LogOn();
```

Used to log the server on, typically this will be called automatically assuming you have set autoLogon to true.
