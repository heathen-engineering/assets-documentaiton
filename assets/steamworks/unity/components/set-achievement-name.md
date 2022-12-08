# Set Achievement Name

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Reads the achievement name from the configured achievement

## Definition

```csharp
[RequireComponent(typeof(TextMeshProUGUI))]
public class SetAchievementName : MonoBehaviour
```

## Fields and Attributes

### Achievement

```csharp
public AchievementObject achievement;
```

The achievement we should load for.

## Methods

### Refresh

```csharp
public void Refresh()
```

Refresh the name.
