---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Favorite Game

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct FavoriteGame
```

Used by the [Matchmaking ](../api/matchmaking.client.md)interface in relation to favorite game servers.

## Fields and Attributes

<table><thead><tr><th width="187.56643368118847">Type</th><th width="183.36921690104845">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>AppId_t</td><td>appId</td><td>The ID of the game</td></tr><tr><td>string</td><td>IpAddress</td><td>string representation of the IP address</td></tr><tr><td>uint</td><td>ipAddress</td><td>Steam native uint version of the IP address</td></tr><tr><td>ushort</td><td>connectionPort</td><td></td></tr><tr><td>ushort</td><td>queryPort</td><td></td></tr><tr><td>DateTime</td><td>lastPlayedOnServer</td><td></td></tr><tr><td>bool</td><td>isHistory</td><td></td></tr></tbody></table>

