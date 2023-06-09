# UGC Community Item

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Returned by UGC Query and related tools and represents the data of a UGC Item aka Workshop Item.

```csharp
public class UserGeneratedContentReadCommunityItem
```

## Definition

### Fields and Attributes

<table><thead><tr><th>Type</th><th width="209.51471669589483">Name</th><th>Notes</th></tr></thead><tbody><tr><td>string</td><td>Title</td><td>The title of the item</td></tr><tr><td>string</td><td>Description</td><td>The description of the item</td></tr><tr><td>AppId_t</td><td>ConsumerApp</td><td>the app this item is meant to be used by</td></tr><tr><td>PublishedFileID_t</td><td>FileId</td><td>The ID of the file</td></tr><tr><td>CSteamID</td><td>Owner</td><td>The id of the Steam User that created the file</td></tr><tr><td>DateTime</td><td>TimeCreated</td><td>The date and time this  item was created</td></tr><tr><td>DateTime</td><td>TimeUpdated</td><td>The most reacent date and time this item was updated</td></tr><tr><td>uint</td><td>UpVotes</td><td>number of times this item has been up voted</td></tr><tr><td>uint</td><td>DownVotes</td><td>number of times this item has been down voted</td></tr><tr><td>float</td><td>VoteScore</td><td>the vote score of this item</td></tr><tr><td>bool</td><td>IsBanned</td><td>if the item is banned</td></tr><tr><td>bool</td><td>IsTagsTruncated</td><td>the tag string was to long and has been truncated</td></tr><tr><td>bool</td><td>IsSubscribed</td><td>True if the item flags contains the subscribed flag</td></tr><tr><td>bool</td><td>IsNeedsUpdated</td><td>True if the item flags contains the needs update flag</td></tr><tr><td>bool</td><td>IsInstalled</td><td>True if the item flags contains the installed flag</td></tr><tr><td>bool</td><td>IsDownloading</td><td>True if the items flags contains the downloading flag</td></tr><tr><td>bool</td><td>IsDownloadPendeing</td><td>True if the items flags contains the download pending flag</td></tr><tr><td>int</td><td>FileSize</td><td>the size of the related file</td></tr><tr><td>EItemState</td><td>StateFlags</td><td>the flags related to the item, e.g subscribed, installed, needs update, etc.</td></tr><tr><td>ERemoteStoragePublishedFileVisibility</td><td>Visibility</td><td>the visibility mode of the item</td></tr><tr><td>string[]</td><td>Tags</td><td>the tags related to the item</td></tr><tr><td>Texture2D</td><td>previewImage</td><td><p>the previewImage found if any.</p><p></p><p>This will be destroyed when this item is deconstructed</p></td></tr><tr><td>string</td><td>previewImageLocation</td><td>The location on disk for the preview image</td></tr><tr><td>SteamUGCDetails_t</td><td>SourceItemDetails</td><td>The native Steamworks details object for this item</td></tr></tbody></table>
