# Rank Change

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct RankChange
```

Used by the Leaderboard system when a user's rank changes.

### Fields and Attributes

<table><thead><tr><th width="220.30993726870204">Type</th><th width="169.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>string</td><td>leaderboardName</td><td>The name of the board</td></tr><tr><td>SteamLeaderboard_t</td><td>leaderboardId</td><td>The id of the board</td></tr><tr><td>LeaderboardEntry</td><td>oldEntry</td><td>The prior entry data</td></tr><tr><td>LeaderboardEntry</td><td>newEntry</td><td>The current entry data</td></tr><tr><td>int</td><td>rankDelta</td><td>The amount of change in rank e.g. new - old</td></tr><tr><td>int</td><td>scoreDelta</td><td>The amount of change in score e.g. new - old</td></tr></tbody></table>

