---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Workshop Browser Simple Item Record

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Displays a list of the clans the user sees e.g. is a member of or otherwise has a relationship with.

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class WorkshopBrowserSimpleItemRecord : MonoBehaviour, 
                                               IWorkshopBrowserItemTemplate
```

## Fields and Attributes

### Preview Image

```csharp
public RawImage previewImage;
```

Display for the primary preview image of the item

### Title Label

```csharp
public TMPro.TextMeshProUGUI titleLabel;
```

Display for the item's title

### Author Label

```csharp
public TMPro.TextMeshProUGUI authorLabel;
```

Display for the name of the author if known

### Vote Fill Image

```csharp
public Image voteFillImage;
```

A simple image that will be set to fill, when the item is loaded its vote ratio will be used to fill this image. This can be used to display the number of stars by creating an image with 5 starts in a row spaced tip to tip over the width of the image. If set to fill from left to right then a ratio of 0.8 would be presented as 4 of the 5 stars filled.

### Tip Title Label

```csharp
public TMPro.TextMeshProUGUI tipTitleLabel;
```

This is the header or "title" of the tooltip window that will show when the user mouses over this item.

### Tip Description Label

```csharp
public TMPro.TextMeshProUGUI tipDescriptionLabel;
```

This is the body of text that will appear in the tooltip window when the user mouses over this item.

### Item

```csharp
public WorkshopItem Item { get; set; }
```

Used to apply the WorkshopItem this entry will represent or read which item was applied.

## Methods

### Load

```csharp
public void Load(WorkshopItem item)
```

sets the item this entry represents
