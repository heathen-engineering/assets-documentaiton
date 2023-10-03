---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Leaderboard User Entry

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Reads the user's record from the referenced [LeaderboardObject ](../scriptable-objects/leaderboard-object.md)and populates a TextMesh Pro label with the rank and score.

This will update as the user's score is updated keeping it up to date with any changes made.

## Fields and Attributes

### Leaderboard

```csharp
public LeaderboardObject leaderboard;
```

A reference to the leaderboard that should be read.

### Score

```csharp
public TextMeshProUGUI score;
```

A reference to a TextMesh Pro label where the user's score will be written.

### Rank

```csharp
public TextMeshProUGUI rank;
```

A reference to a TextMesh Pro lable where the user's rank will be written.
