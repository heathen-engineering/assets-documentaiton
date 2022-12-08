# Set Achievement Icon

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

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
