# Leaderboard Entry UI Record

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

A simple implementation of the [ILeaderboardEntryDisplay ](../../unity/interfaces/ileaderboardentrydisplay.md)interface.

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

From the [ILeaderboardEntryDisplay ](../../unity/interfaces/ileaderboardentrydisplay.md)interface and is used by the [Leaderboard UI List](leaderboard-ui-list.md) to set the entry that this object will represent and thus updating all the UI elements.
