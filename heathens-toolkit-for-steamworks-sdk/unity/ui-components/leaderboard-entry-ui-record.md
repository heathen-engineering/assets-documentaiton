---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Leaderboard Entry UI Record

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

A simple implementation of the [ILeaderboardEntryDisplay ](../programming-tools/ileaderboardentrydisplay.md)interface.

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class LeaderboardEntryUIRecord : MonoBehaviour,
                                        ILeaderboardEntryDisplay
```

## Fields and Attributes

### Avatar

```csharp
public SetUserAvatar avatar;
```

A [SetUserAvatar ](set-user-avatar.md)reference which will be used to display this record's owner's avatar.

### User Name

```csharp
public TMProSetUserName userName;
```

A [TMProSetUserName ](set-user-name.md)reference which will be used to display this record's owner's name.

### Score

```csharp
public TextMeshProUGUI score;
```

A TextMesh Pro label reference that will be used to display the record's owner's score.

### Rank

```csharp
public TextMeshProUGUI rank;
```

A TextMesh Pro label reference that will be used to display the record's owner's rank.

### Entry

```csharp
public LeaderboardEntry Entry { get; set; }
```

From the [ILeaderboardEntryDisplay ](../programming-tools/ileaderboardentrydisplay.md)interface and is used by the [Leaderboard UI List](leaderboard-ui-list.md) to set the entry that this object will represent and thus updating all the UI elements.
