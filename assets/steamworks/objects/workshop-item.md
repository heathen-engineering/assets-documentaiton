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

## Methods

### Get

WorkshopItem objects are "get" by query, the Get methods are static methods that help you create a [UgcQuery ](ugc-query.md)to fetch specific items. This is just a shortcut to the [UgcQuery ](ugc-query.md)get methods, see [UgcQuery ](ugc-query.md)documentation for more details.

### Download Preview Image

Starts the download of the preview image

```csharp
public void DownloadPreviewImage()
```

### Download Item

```csharp
public bool DownloadItem(bool highPriority)
```

Typically Steam will download the item when it's convenient to do so and won't usually download while a game is running. High Priority flag simply indicates that Steam should download the item as soon as it can.

### Subscribe

```csharp
public void Subscribe(Action<RemoteStorageSubscribePublishedFileResult_t, bool> callback)
```

Causes the item to be marked as subscribed, the callback indicates the results&#x20;

<pre class="language-csharp"><code class="lang-csharp"><strong>void Callback(RemoteStorageSubscribePublishedFileResult_t results, bool ioError)
</strong>{
    //Do Work
}
</code></pre>

### Unsubscribe

```csharp
public void Unsubscribe(Action<RemoteStorageUnsubscribePublishedFileResult_t, bool> callback)
```

Causes the item to be marked as unsubscribed, the callback indicates the results&#x20;

<pre class="language-csharp"><code class="lang-csharp"><strong>void Callback(RemoteStorageSubscribePublishedFileResult_t results, bool ioError)
</strong>{
    //Do Work
}
</code></pre>

### Set Vote

```csharp
public void SetVote(bool voteUp, Action<SetUserItemVoteResult_t, bool> callback)
```

Sets the user's vote for this item, the callback indicates the results

<pre class="language-csharp"><code class="lang-csharp"><strong>void Callback(SetUserItemVoteResult_t results, bool ioError)
</strong>{
    //Do Work
}
</code></pre>

## Update Methods

If the local user is the owner of the item they can modify the items values, the following methods are only applicable to the item's owners and will not work as intended for any other user.

### Update Title

```csharp
public void UpdateTitle(string value, 
                        string changeNote, 
                        Action<SubmitItemUpdateResult_t, bool> callback)
```

Use to update the item's title, the callback will indicate the results of the operation, the bool indicates error, for example:

<pre class="language-csharp"><code class="lang-csharp"><strong>void Callback(SubmitItemUpdateResult_t results, bool ioError)
</strong>{
    //Do Work
}
</code></pre>

Update Title has a single overload where you can indicate the language associated with the title.

```csharp
public void UpdateTitle(string value, 
                        LanguageCodes language, 
                        string changeNote, 
                        Action<SubmitItemUpdateResult_t, bool> callback)
```

### Update Description

```csharp
public void UpdateDescription(string value, 
                        string changeNote, 
                        Action<SubmitItemUpdateResult_t, bool> callback)
```

Use to update the item's description, the callback will indicate the results of the operation, the bool indicates error, for example:

```csharp
void Callback(SubmitItemUpdateResult_t results, bool ioError)
{
    //Do Work
}
```

Update Description has a single overload where you can indicate the language associated with the title.

```csharp
public void UpdateDescription(string value, 
                        LanguageCodes language, 
                        string changeNote, 
                        Action<SubmitItemUpdateResult_t, bool> callback)
```

### Update Content

This can be used to update the preview image or the contents of the items folder

```csharp
//For content folder
public void UpdateContent(DirectoryInfo value, 
                          string changeNote, 
                          Action<SubmitItemUpdateResult_t, bool> callback)
```

```csharp
//For preview image
public void UpdateContent(FileInfo value, 
                          string changeNote, 
                          Action<SubmitItemUpdateResult_t, bool> callback)
```

The callback will indicate the results or error if any

```csharp
void Callback(SubmitItemUpdateResult_t results, bool ioError)
{
    //Do Work
}
```

### Update Metadata

Update the metadata linked to the object

```csharp
public void UpdateMetadata(string value, 
                           string changeNote, 
                           Action<SubmitItemUpdateResult_t, bool> callback)
```

The callback will indicate the results or error if any

```csharp
void Callback(SubmitItemUpdateResult_t results, bool ioError)
{
    //Do Work
}
```

### Update Tags

Update the tags linked to the object

```csharp
public void UpdateTags(string[] value, 
                       string changeNote, 
                       Action<SubmitItemUpdateResult_t, bool> callback)
```

The callback will indicate the results or error if any

```csharp
void Callback(SubmitItemUpdateResult_t results, bool ioError)
{
    //Do Work
}
```

### Delete Item

Requests the delet of this item

```csharp
public void DeleteItem(Action<DeleteItemResult_t, bool> callback)
```

The callback will indicate the results or error if any

```csharp
void Callback(DeleteItemResult_t results, bool ioError)
{
    //Do Work
}
```
