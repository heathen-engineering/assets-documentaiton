---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Workshop Item Data

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using HeathenEngineering.SteamworksIntegration;
```

```csharp
public struct WorkshopItemData
```

A helper tool that allows you to pre-define all of the typical fields of a Steam User Generated Content item (aka a Workshop Item) for quick and easy creation or update. see the method for details.

## Definition

Used with the User Generated Content interface for 1 line creation of workshop items.

## Fields and Attributes

### Published File Id

```csharp
public PublishedFileId_t? publishedFileId
```

The published file ID is to be updated. This can be null and would be in the case of a create, if you are however updating an item this should be populated with the ID of the file to be updated

> Note the ? at the end of the data type, this is a C# feature and indicates that this is a "Nullable" attribute e.g. Nullable\<PublishedFileId\_t> in this case.

### App Id

```csharp
public AppData appId
```

The consume and creating app ID of the item.

### Title

```csharp
public string title
```

The title of the item.

### Description

```csharp
public string description
```

The description of the item.

### Content

```csharp
public DirectoryInfo content
```

The folder where the content is located is used when creating and updating an item.

### Preview

```csharp
public FileInfo preview
```

The file to be used as the preview image should be a .jpg or .png file and its size must be smaller than that defined in the app's remote storage settings.

### Metadata

```csharp
public string metadata
```

The metadata associated with the file if any.

### Tags

```csharp
public string[] tags
```

The set of tags associated or to be associated with the item.

### Visibility

```csharp
public ERemoteStoragePublishedFileVisibility visibility
```

The visibility setting to apply to the file when created or updated.

### Is Valid

```csharp
public bool IsValid => get;
```

Returns true if all required fields are set and conform to Valve's basic requirements.

* App ID is set to a valid app
* title is not null or empty
* title length is less than the max allowed by Valve (8000)
* description is not null or empty
* description length is less than the max allowed by Valve (8000)
* metadata if populated length is less than the max allowed by Valve (5000)
* preview is not null and file exists
* content is not null and folder exists
* no tag length is greater than 255

## Methods

### Create

```csharp
public bool Create(Action<WorkshopItemDataCreateStatus> callback = null)
```

or

```csharp
public bool Create(WorkshopItemPreviewFile[] additionalPreviews, 
                   string[] additionalYouTubeIds, 
                   WorkshopItemKeyValueTag[] additionalKeyValueTags, 
                   Action<WorkshopItemDataCreateStatus> callback = null)
```

Creates a workshop item with the fields defined in the structure, optionally with additional preview images, videos and key value tags.

### Update

```csharp
public bool Update(Action<WorkshopItemDataUpdateStatus> callback = null)
```

or

```csharp
public bool Update(WorkshopItemPreviewFile[] additionalPreviews, 
                   string[] additionalYouTubeIds, 
                   WorkshopItemKeyValueTag[] additionalKeyValueTags, 
                   Action<WorkshopItemDataUpdateStatus> callback = null)
```

Assuming the publishedFileId is a valid file that the user owns this will update that file&#x20;

### Get

```csharp
public static void Get(PublishedFileId_t file, Action<WorkshopItem> callback)
```

Gets the WorkshopItem for the indicated file.

### Get Subscribed

```csharp
public static void GetSubscribed(bool withLongDescription, 
                                 bool withMetadata, 
                                 bool withKeyValueTags, 
                                 bool withAdditionalPreviews, 
                                 uint withPlayTimeStatsInDays, 
                                 Action<List<WorkshopItem>> callback)
```

Gets the subscribed items with the additional arguments requested.
