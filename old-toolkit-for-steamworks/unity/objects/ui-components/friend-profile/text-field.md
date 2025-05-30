---
cover: ../../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Text Field

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

A sub struct used by the built in [FriendProfile ](./)to define the settings for text fields on that control. The TextField struct simply provides a pointer to an text to be used a flag to enable or disable the use of coloring options and the values for the color options to be used.

```csharp
public struct FriendProfile.ImageField
```

## Fields and Attributes

### image

```csharp
public Image image
```

A reference to the image to be used

### useStatusColors

```csharp
public bool useStatusColors
```

A boolean indicating rather or not the system should apply colouring to the image based on status.

### inThisGame

```csharp
public Color inThisGame
```

The color to be applied to the text when the related user is found to be playing the same App ID as the App ID for this instance of Steam API.

### inOtherGame

```csharp
public Color inOtherGame
```

The color to be applied to the text when the related user is found to be in an App other than the App for this instance of Steam API.

### isOnlineActive

```csharp
public Color isOnlineActive
```

The color to be applied to the text when the related user is not in a game/app but is online and is active.

### isOnlineInactive

```csharp
public Color isOnlineInactive
```

The color to be applied to the text when the related user is not in a game/app but is online and is not active.

### isOffline

```csharp
public Color isOffline
```

The color to be applied to the text when the related user is not online at all.

## Methods

### SetValue

```csharp
public void SetValue(bool inGame, bool inThisGame, EPersonaState state)
```

Called when setting the value of the text and provides information about the related user.
