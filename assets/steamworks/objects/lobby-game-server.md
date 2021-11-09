# Lobby Game Server

## Definition

```csharp
public struct LobbyGameServer
```

Represents Game Server connection information as used by the Steam Lobby system.

Note a server will always have either or both IP/Port and ID, it will never have none. ID e.g. CSteamID is used by SteamNetworking and SteamNetworkingSockets for connections. IP/Port is more offten used with 3rd party transports such as KCP, TCP, UDP, etc. A server may have both as a server may handle both SteamNetworkign and other 3rd party connections.

### Fields and Attributes

| Type     | Name      | Comment                                                             |
| -------- | --------- | ------------------------------------------------------------------- |
| CSteamID | id        | The id of the Steam Game Server or of the Steam User acting as host |
| string   | IpAddress | string parse of the uint IP address                                 |
| uint     | ipAddress | The ip address as Steam would nativly handle it                     |
| ushot    | port      | The connection port                                                 |

