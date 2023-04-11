# Workshop Item Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

A simple struct making it easier to create and update workshop items.

## Definition

```csharp
public struct WorkshopItemData
```

Used with the User Generated Content interface for 1 line creation of workshop items.

## Fields and Attributes

### publishedFileId

```csharp
public PublishedFileId_t? publishedFileId
```

The published file ID if any,&#x20;

> Note the ? at the end of the data type, this is a C# feature and indicates that this is a "Nullable" attribute e.g. Nullable\<PublishedFileId\_t> in this case.

### appId

```csharp
public AppData appId
```

The app this item is related to

### title

```csharp
public string title
```

The title of the item

### description

```csharp
public string description
```

The description of the item

### content

```csharp
public DirectoryInfo content
```

The folder where the content is located, this is used when creating and updating an item

### preview

```csharp
public FileInfo preview
```

The file to be used as the preview image, this should be a .jpg or .png file and its size must be smaller than that defined in the app's remote storage settings.

### metadata

```csharp
public string metadata
```

The metadata associated with the file if any

### tags

```csharp
public string[] tags
```

The set of tags associated or to be associated with the item

### visibility

```csharp
public ERemoteStoragePublishedFileVisibility visibility
```

The visibility setting to apply to the file when created or updated.

### IsValid

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
public bool Update(Action<WorkshopItemDataCreateStatus> callback = null)
```

or

```csharp
public bool Update(WorkshopItemPreviewFile[] additionalPreviews, 
                   string[] additionalYouTubeIds, 
                   WorkshopItemKeyValueTag[] additionalKeyValueTags, 
                   Action<WorkshopItemDataCreateStatus> callback = null)
```

Assuming the publishedFileId is a valid file that the user owns this will update that file&#x20;

### Get

```csharp
public static void Get(PublishedFileId_t file, Action<WorkshopItem> callback)
```

Gets the WorkshopItem for the indicated file.
