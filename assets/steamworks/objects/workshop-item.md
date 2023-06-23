# Workshop Item

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Returned by UGC Query and related tools and represents the data of a UGC Item aka Workshop Item.

```csharp
public class WorkshopItem
```

## Fields and Attributes

### Title

```csharp
public string Title => get;
```

The title of the item

### Description

```csharp
public string Description => get;
```

The description of the item

### Consumer App

```csharp
public AppData ConsumerApp => get;
```

The app this item is meant to be used by

### FileId

```csharp
public PublishedFileId_t FileId => get;
```

The Steam native ID for this item's "file"

### Owner

```csharp
public UserData Owner => get;
```

The user that "owns" this item, typically the "author"

### Time Created

```csharp
public DateTime TimeCreated => get;
```

The time stamp this item was created on

### Time Updated

```csharp
public DateTime TimeUpdated => get;
```

The time stamp of this item's last update

### Up Votes

```csharp
public uint UpVotes => get;
```

The current number of up votes this item has

### Down Votes

```csharp
public uint DownVotes => get;
```

The current number of down votes this item has

### Vote Score

```csharp
public float VoteScore => get;
```

The vote score applied to this item

### Is Banned

```csharp
public bool IsBanned => get;
```

Has this item been banned

### Is Tags Truncated

```csharp
public bool IsTagsTruncated => get;
```

Is the tags list on this item truncated for length

### Is Subscribed

```csharp
public bool IsSubscribed => get;
```

Is the local user subscribed to this item

### Is Needs Update

```csharp
public bool IsNeedsUpdate => get;
```

Does this item need to be updated

### Is Installed

```csharp
public bool IsInstalled => get;
```

Is this item currently installed

### Is Downloading

```csharp
public bool IsDownloading => get;
```

is this item currently downloading

### Is Download Pending

```csharp
public bool IsDownloadPending =-> get;
```

Is this item pending download

### DownloadCompletion

```csharp
public float DownloadCompletion => get;
```

If this item is downloading how far along is it

### File Size

```csharp
public int FileSize => get;
```

The "file size" as reported by Valve for this item

### Folder Path

```csharp
public DirectoryInfo FolderPath => get;
```

The directory where this items content is located

### State Flags

```csharp
public EItemState StateFlags => get;
```

The state flags associated with this item, see [Valve's Steam API documentation](https://partner.steamgames.com/doc/api/ISteamUGC#EItemState) for more details.

### Visibility

```csharp
public ERemoteStoragePublishedFileVisibility Visibility => get;
```

The visibility status of the item, see [Valve's Steam API documentation](https://partner.steamgames.com/doc/api/ISteamRemoteStorage#ERemoteStoragePublishedFileVisibility) for more details.

### Tags

```csharp
public string[] Tags => get;
```

The array of tags if any, this causes a new array to be created each time its read so cash the value and work with the cash where needed.

### Preview Image

```csharp
public Texture2D previewImage;
```

The main preview image if known

### Preview Image Location

```csharp
public string previewImageLocation;
```

The location of the preview image's file if known

### Source Item Details

```csharp
public SteamUGCDetails_t SourceItemDetails => get;
```

The Steam native details item

### Metadata

```csharp
public string metadata;
```

The metadata for the item if any and if included in the reading query

### Key Value Tags

```csharp
public StringKeyValuePair[] keyValueTags;
```

The key value tags associated with the item if any and if known

## Events

### Preview Image Updated

```csharp
public UnityEvent previewImageUpdated;
```

A standard UnityEvent which is invoked when/if the items preview image is updated and reported from Steam or when the file is loaded from disk if known. This can be used to trigger an update of display of the item preview image.
