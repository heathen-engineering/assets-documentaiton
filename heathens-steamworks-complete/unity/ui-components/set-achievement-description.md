---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Set Achievement Description

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Reads the achievement name from the configured achievement

## Definition

```csharp
[RequireComponent(typeof(TextMeshProUGUI))]
public class SetAchievementDescription : MonoBehaviour
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

Refresh the description.
