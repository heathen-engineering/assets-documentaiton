---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Lobby Game Server

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct LobbyGameServer
```

Represents Game Server connection information as used by the Steam Lobby system.

Note a server will always have either or both IP/Port and ID, it will never have none. ID e.g. CSteamID is used by SteamNetworking and SteamNetworkingSockets for connections. IP/Port is more offten used with 3rd party transports such as KCP, TCP, UDP, etc. A server may have both as a server may handle both SteamNetworkign and other 3rd party connections.

### Fields and Attributes

<table><thead><tr><th width="187.56643368118847">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>CSteamID</td><td>id</td><td>The id of the Steam Game Server or of the Steam User acting as host</td></tr><tr><td>string</td><td>IpAddress</td><td>string parse of the uint IP address</td></tr><tr><td>uint</td><td>ipAddress</td><td>The ip address as Steam would nativly handle it</td></tr><tr><td>ushot</td><td>port</td><td>The connection port</td></tr></tbody></table>

