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

| Type                                  | Name                 | Notes                                                                                                     |
| ------------------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------- |
| string                                | Title                | The title of the item                                                                                     |
| string                                | Description          | The description of the item                                                                               |
| AppId\_t                              | ConsumerApp          | the app this item is meant to be used by                                                                  |
| PublishedFileID\_t                    | FileId               | The ID of the file                                                                                        |
| CSteamID                              | Owner                | The id of the Steam User that created the file                                                            |
| DateTime                              | TimeCreated          | The date and time this  item was created                                                                  |
| DateTime                              | TimeUpdated          | The most reacent date and time this item was updated                                                      |
| uint                                  | UpVotes              | number of times this item has been up voted                                                               |
| uint                                  | DownVotes            | number of times this item has been down voted                                                             |
| float                                 | VoteScore            | the vote score of this item                                                                               |
| bool                                  | IsBanned             | if the item is banned                                                                                     |
| bool                                  | IsTagsTruncated      | the tag string was to long and has been truncated                                                         |
| bool                                  | IsSubscribed         | True if the item flags contains the subscribed flag                                                       |
| bool                                  | IsNeedsUpdated       | True if the item flags contains the needs update flag                                                     |
| bool                                  | IsInstalled          | True if the item flags contains the installed flag                                                        |
| bool                                  | IsDownloading        | True if the items flags contains the downloading flag                                                     |
| bool                                  | IsDownloadPendeing   | True if the items flags contains the download pending flag                                                |
| int                                   | FileSize             | the size of the related file                                                                              |
| EItemState                            | StateFlags           | the flags related to the item, e.g subscribed, installed, needs update, etc.                              |
| ERemoteStoragePublishedFileVisibility | Visibility           | the visibility mode of the item                                                                           |
| string\[]                             | Tags                 | the tags related to the item                                                                              |
| Texture2D                             | previewImage         | <p>the previewImage found if any.</p><p></p><p>This will be destroyed when this item is deconstructed</p> |
| string                                | previewImageLocation | The location on disk for the preview image                                                                |
| SteamUGCDetails\_t                    | SourceItemDetails    | The native Steamworks details object for this item                                                        |
