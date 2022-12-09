# Lobby Game Server

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

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

