---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Avg Rate Stat

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class AvgRateStatObject : StatObject
```

Represents a AvgRat stat, consult the Steam Documentation for the specific use cases for each of the stat types

{% embed url="https://partner.steamgames.com/doc/features/achievements" %}

## Fields and Attributes

### Value

```csharp
public float Value => get
```

Reads the current value of the stat

## Methods

{% hint style="danger" %}
Other methods are available but should not be used and exist only for compatability with the generic StatObject interface.
{% endhint %}

### Update Stat

```csharp
public void UpdateAvgRateStat(value, length);
```

Updates the stat

### Store Stats

```csharp
public void StoreStas();
```

Calls Store Stats on the the Steam API
