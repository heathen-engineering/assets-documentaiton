# Rank Change

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct RankChange
```

Used by the Leaderboard system when a user's rank changes.

### Fields and Attributes

| Type                | Name            | Comment                                      |
| ------------------- | --------------- | -------------------------------------------- |
| string              | leaderboardName | The name of the board                        |
| SteamLeaderboard\_t | leaderboardId   | The id of the board                          |
| LeaderboardEntry    | oldEntry        | The prior entry data                         |
| LeaderboardEntry    | newEntry        | The current entry data                       |
| int                 | rankDelta       | The amount of change in rank e.g. new - old  |
| int                 | scoreDelta      | The amount of change in score e.g. new - old |

