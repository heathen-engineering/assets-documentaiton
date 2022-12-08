# Favorite Game

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct FavoriteGame
```

Used by the [Matchmaking ](../api/matchmaking.md)interface in relation to favorite game servers.

## Fields and Attributes

| Type     | Name               | Comment                                     |
| -------- | ------------------ | ------------------------------------------- |
| AppId\_t | appId              | The ID of the game                          |
| string   | IpAddress          | string representation of the IP address     |
| uint     | ipAddress          | Steam native uint version of the IP address |
| ushort   | connectionPort     |                                             |
| ushort   | queryPort          |                                             |
| DateTime | lastPlayedOnServer |                                             |
| bool     | isHistory          |                                             |

