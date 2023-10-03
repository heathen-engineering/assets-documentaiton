---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Set Achievement Icon

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Reads the achievement icon image from the Steam backend. This will display the locked or unlocked image depending on the current state of the achievement for the user.

## Definition

```csharp
[RequireComponent(typeof(UnityEngine.UI.RawImage))]
public class SetAchievementIcon : MonoBehaviour
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

Refresh the image, this will automatically be called anytime Valve notifies the game of a change such as on Set, Clear or Reset.
