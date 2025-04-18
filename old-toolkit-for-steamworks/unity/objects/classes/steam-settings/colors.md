---
cover: ../../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Colors

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

This simply defines common Steam colors

## Definition

```csharp
public class SteamSettings : ScriptableObject
{
    public static class Colors;
}
```

### Fields and Attributes

```csharp
public static Color SteamBlue = new Color(0.2f, 0.60f, 0.93f, 1f);
public static Color SteamGreen = new Color(0.2f, 0.42f, 0.2f, 1f);
public static Color BrightGreen = new Color(0.4f, 0.84f, 0.4f, 1f);
public static Color HalfAlpha = new Color(1f, 1f, 1f, 0.5f);
public static Color ErrorRed = new Color(1, 0.5f, 0.5f, 1);
```
