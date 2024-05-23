---
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# ILeaderboardEntryDisplay

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Used by the Leaderboard UI List when instantiating records. This can be inherited from to create custom Leaderboard Entry Display's similar to the Leaderboard Display Entry provided in the asset.

## Fields and Attributes

### Entry

```csharp
public LeaderboardEntry Entry { get; set; }
```

This will be set by the Leaderboard UI List when instantiating a record and should update the UI elements of the entry accordingly.
