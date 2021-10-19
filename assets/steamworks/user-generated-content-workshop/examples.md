---
description: User Generated Content (Workshop) examples
---

# Examples

## Create Item

```csharp
SteamSettings.UGC.CreateItem(appId,
                title,
                description,
                changeNote,
                contentFolderPath,
                previewImagePath,
                tags,
                fileType,
                visibility,
                completionCallback);
```

| Title               | Parameter | Description                                                                                                                                                                                                                                                                                 |
| ------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| App Id              | Required  | The ID of the application this item can be used with                                                                                                                                                                                                                                        |
| Title               | Optional  | The display name / title of the item as it will appear in Steam's Workshop                                                                                                                                                                                                                  |
| Description         | Optional  | The description text that will be showed with the item                                                                                                                                                                                                                                      |
| Change Note         | Optional  | The annotation applied to the item on update                                                                                                                                                                                                                                                |
| Content Folder Path | Required  | The folder path (not a file it must be a folder) that Valve's Steam client should upload as the content of the item                                                                                                                                                                         |
| Preview Image Path  | Required  | The file path (not a folder it must be a file) that Valve's Steam client should upload as the preview of the item                                                                                                                                                                           |
| Tags                | Optional  | A list of string values to be applied as tags on update                                                                                                                                                                                                                                     |
| File Type           | Required  | <p>Defaults to k_EWorkshopFileTypeCommunity</p><p>This is the type or kind of UGC file to be created ... the default is the appropriate type for a Workshop item</p>                                                                                                                        |
| Visibility          | Required  | <p>Defaults to k_ERemoteStoragePublishedFileVisibilityPrivate</p><p>This sets the visibility of the item and in general should start as private (The default) the user can set this in the Steam client later after they have accepted the TOC and performed other administrative tasks</p> |
| Completion Callback | Optional  | This is a method that will be invoked when the process has completed                                                                                                                                                                                                                        |

## Query For Items

The `WorkshopItemQuery` class greatly simplifies the process of querying for UGC records. You can simply create a `WorkshoItemQuery` and execute it in most cases with no additional steps required.

```csharp
var query = WorkshopItemQuery.Create(...);
query.Execute(callback);
```

The `Create` method has 3 overloads as described below. Once you have created a query the query can be modified with further arguments as shown below.

### Create Query All

Used to return lists of all UGC items that match a given type

```csharp
Create(queryType, matchingType, creatorApp, consumerApp);
```

#### Parameters

| Type                | Name         | Note                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| EUGCQuery           | queryType    | <p>Describes the type of query</p><ul><li>Rank By Vote</li><li>Rank By Publication Date</li><li>Accepted For Game Ranked By Acceptance Date</li><li>Ranked By Trend</li><li>Favorited By Friends Ranked By Publication Date</li><li>Created By Friends Ranked By Publication Date</li><li>Ranked By Number of Times Reported</li><li>Created By Followed Users Ranked By Publication Date</li><li>Not Yet Rated</li><li>Ranked By Total Votes Ascending </li><li>Ranked By Votes Up</li><li>Ranked By Text Search</li><li>Ranked By Total Unique Subscriptions</li><li>Ranked By Playtime Trend</li><li>Ranked By Total Playtime</li><li>Ranked By Average Playtime Trend</li><li>Ranked By Lifetime Average Playtime</li><li>Ranked By Playtime Sessions Trend</li><li>Ranked BNy Lifetime Playtime Sessions</li></ul> |
| EUGCMatchingUGCType | matchingType | <p>Describes the type to match for</p><ul><li>Items</li><li>Items MTX</li><li>Items Ready To Use</li><li>Collections</li><li>Artwork</li><li>Videos</li><li>Screenshots</li><li>All Guides</li><li>Web Guides</li><li>Integrated Guides</li><li>Usable In Game</li><li>Controller Bindings</li><li>Game Managed Items</li><li>All (not available for this query type)</li></ul>                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| AppId\_t            | creatorApp   | The app that created the UGC ... this is typically your game's App Id                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| AppId\_t            | consumerApp  | The app that is intended to use the UGC. This is typically your game's App Id                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

### Create Detail Query

Used to return details for a specific set of UGC items

```csharp
Create(fileIds);
```

#### Parameters

| Type                             | Name    | Note                                                  |
| -------------------------------- | ------- | ----------------------------------------------------- |
| IEnumerable\<PublishedFileId\_t> | fileIds | A collection of the file IDs to fetch the details for |

### Create User Query

Used to return UGC items related to a given User list

```csharp
Create(accountId, listType, matchingType, creatorApp, consumerApp);
```

#### Parameters

| Type                  | Name         | Note                                                                                                                                                                                                                                                                                                                                                                                |
| --------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AccountID\_t          | account      | The account of the user this list query should be related to. The AccountID for a user can be had from the user's CSteamID by calling steamId.GetAccountId();                                                                                                                                                                                                                       |
| EUserUGCList          | listType     | <p>The list to query options include:</p><ul><li>Published</li><li>Voted On</li><li>Voted Up</li><li>Voted Down</li><li>Will Vote Later</li><li>Favorited</li><li>Subscribed</li><li>Used Or Played</li><li>Followed</li></ul>                                                                                                                                                      |
| EUGCMatchingUGCType   | matchingType | <p>Describes the type to match</p><ul><li>Items</li><li>Items MTX</li><li>Items Ready To Use</li><li>Collections</li><li>Artwork</li><li>Videos</li><li>Screenshots</li><li>All Guides</li><li>Web Guides</li><li>Integrated Guides</li><li>Usable In Game</li><li>Controller Bindings</li><li>Game Managed Items</li><li>All (only available for this query type)</li></ul><p></p> |
| EUserUGCListSortOrder | sortOrder    | <p>The method to sort the results by</p><ul><li>Creation Order Descending</li><li>Creation Order Ascending</li><li>Title Ascending</li><li>Last Updated Descending</li><li>Subscription Date Descending</li><li>Vote Score Descending</li><li>For Moderation</li></ul>                                                                                                              |
| AppId\_t              | creatorApp   | The app used to create the UGC. This is usually your game's App Id                                                                                                                                                                                                                                                                                                                  |
| AppId\_t              | consumerApp  | The app meant to consume the UGC. This is usually your game's App ID                                                                                                                                                                                                                                                                                                                |

### Set Search Text

This is the most common thing to set on a search. Its a simple string just as you might type into the Search box in the Workshop, and will be used by Valve's query when filtering down results. The implementation for that filter is defined by Valve and subject to change but typically favors title and description.

```csharp
query.SetSearchText(string text);
```

### Set Language

Set the language to query for

```csharp
query.SetLanguage(string language);
```

### Set Match Any Tag

Only relevant when querying for all UGC type which is its self only relevant when querying user

```csharp
query.SetMatchAnyTag(bool anyTag);
```

### Set Ranked By Trend Days

Only relevant for trend type queries this is the trend over X days; for example if you want the trend over the past 30 days i.e. the monthly trend then the value would be 30.

```csharp
query.SetRankedByTrendDays(uint days);
```

### Set Return Additional Previews

```csharp
query.SetReturnAdditionalPreviews(bool additionalPreviews);
```

### Set Return Children

```csharp
query.SetReturnChildren(bool returnChildren);
```

### Set Return Key Value tags

```csharp
query.SetReturnKeyValueTags(bool tags);
```

### Set Return Long Description

```csharp
query.SetReturnLongDescription(bool longDescription);
```

### Set Return Metadata

```csharp
query.SetReturnMetadata(bool metadata);
```

### Set Return Only IDs

This will cause the results to only contain the file ids.

```csharp
query.SetReturnOnlyIDs(bool onlyIds);
```

### Set Return Playtime Stats

```csharp
query.SetReturnPlaytimeStats(uint days);
```

### Set Return Total Only

This will cause the results to only contain the total count of records that matched the query.

```csharp
query.SetReturnTotalOnly(bool totalOnly);
```

## Get Subscribed Items

```csharp
var results = SteamSettings.UGC.GetSubscribedItems();
```

This returns a list of `PublishedFileId_t` being the files that the user is subscribed to.

The following examples assume you are operating on one of these returned items e.g.&#x20;

```csharp
foreach(var item in results)
    ...
```

### Get item state

```csharp
var state = SteamSettings.UGC.GetItemState(item);
```

This value indicates the state of the item

| Value                        | Description                                                                                           |
| ---------------------------- | ----------------------------------------------------------------------------------------------------- |
| k\_EItemStateNone            | item not tracked on client                                                                            |
| k\_EItemStateSubscribed      | current user is subscribed to this item. Not just cached                                              |
| k\_EItemStateLegacyItem      | item was created with ISteamRemoteStorage                                                             |
| k\_EItemStateInstalled       | item is installed and usable (but maybe out of date)                                                  |
| k\_EItemStateNeedsUpdate     | items needs an update. Either because it's not installed yet or creator updated content               |
| k\_EItemStateDownloading     | item update is currently downloading                                                                  |
| k\_EItemStateDownloadPending | DownloadItem() was called for this item, content isn't available until DownloadItemResult\_t is fired |

### Get Item Install Information

```
var success = SteamSettings.UGC.GetItemInstallInfo(item,
                                out ulong sizeOnDisk,
                                out string folderPath,
                                out DateTime timeStamp);
```

This should only be used on items whose state is `k_EItemStateInstalled`. The folder path output is the UNC folder path where the content can be found.

### Download Item

```csharp
var success = SteamSettings.UGC.DownloadItem(item, useHighPriority);
```

If you set as high priority then other downloads will be paused until this finishes. The `evtItemDownloaded` event will be invoked when the download completes.

```csharp
SteamSettings.UGC.evtItemDownloaded.AddListener(HandleDownloadCompleted);
```

This assumes the `HandleDownloadCompleted` method looks similar to&#x20;

```csharp
void HandleDownloadCompleted(DownloadItemResult_t result)
{
    if(SteamSettings.UGC.GetItemInstallInfo(result.m_nPublishedFileId,
                                            out ulong _,
                                            out string folderPath,
                                            out DateTime _))
    {
        Debug.Log("You can find me here " + folderPath);
    }
    else
    {
        Debug.LogError("Something didn't go right :( ");
    }
}
```

### Vote on item

```csharp
SteamSettings.UGC.SetUserItemVote(item, likedIt);
```

the bool value `likedIt` indicates a positive or negative vote on the item.

## Update Item

Updating a UGC item the player is the author of is a multi step process. First you will need to get the File ID of the item you wish to perform the update on.

### Fetch File ID's of Authored UGC

```csharp
//This fetches the account ID of this user
var accountId = SteamSettings.Client.user.SteamId.GetAccountID();

//This gets the user's list of published items
var listType = EUserUGCList.k_EUserUGCList_Published;

//This type only works for this type of query and returns all UGC item types
var matchType = EUGCMatchingUGCType.k_EUGCMatchingUGCType_All;

//Usually this app is the creator app
var creatorApp = SteamSettings.ApplicationId;

//Usually this app is the consumer app as well
var consumerApp = creatorApp;

...

var query= WorkshopItemQuery.Create( accountId,
                                     listType,
                                     matchType,
                                     creatorApp,
                                     consumerApp,
                                     currentPage);
```

Once you have your query simply execute it

```csharp
var success = query.Execute(HandleResults);
```

Handling the results would look like such

```csharp
private void HandleResults(WorkshopItemQuery query)
{
    foreach (var result in query.ResultsList)
    {
         //TODO: use the result
    }
    else
    {
        //Clean up when your done with the results
        query.Dispose();
    }
}
```

### Starting an Update

Now that we have the file id that we would want to perform the update on, we are ready to start the update process. That is we need to tell Valve we intend to update this item and to give us an update handle for it

```csharp
var updateHandle = SteamSettings.UGC.StartItemUpdate(creatorApp, fileId);
```

### Update the deisried fields

Once we have the update handle we use it to set the desired fields

#### Set Item Content

This is the folder path where the UGC content can be found, e.g. its a UNC folder path on the local machine where Steam should look for the content to upload to the UGC file.

```csharp
SteamSettings.UGC.SetItemContent(updateHandle, folderPath);
```

#### Set Item Description

Sets the item's description

```csharp
SteamSettings.UGC.SetItemDescription(updateHandle, description);
```

#### Set Item Metadata

Sets the item's metadata

```csharp
SteamSettings.UGC.SetItemMetadata(updateHandle, metadata);
```

#### Set Item Preview

Sets the item's preview

```csharp
SteamSettings.UGC.SetItemPreview(updateHandle, previewImagePath);
```

#### Set Item Tags

Sets the item's tags

```csharp
SteamSettings.UGC.SetItemTags(updateHandle, tagList);
```

#### Set Item Title

Sets the item's title

```csharp
SteamSettings.UGC.SetItemTitle(updateHandle, title);
```

#### Set Item Update Language

Sets the item update language

```csharp
SteamSettings.UGC.SetItemUpdateLanguage(updateHandle, language);
```

#### Set Item Visibility

Sets the item's visibility

```csharp
//Options include
// Public
// Friend Only
// Private
// Unlisted
ERemoteStoragePublishedFileVisibility visibility;

SteamSettings.UGC.SetItemVisibility(updateHandle, visibility);
```

#### Add Item Key Value Tag

Adds a key value tag to the item

```csharp
SteamSettings.UGC.AddItemKeyValueTag(updateHandle, key, value);
```

#### Add Item Preview File

Adds an additional preview file of an indicated type.

```csharp
EItemPreviewType type;
//Options include
// Image
// YouTubeVideo
// Sketchfab
// EnvironmentMap_HorizontalCross
// EnvironmentMap_LatLong

SteamSettings.UGC.AddItemPreviewFile(updateHandle, filePath, type);
```

#### Add Item Preview Video

This expects the video ID as used by YouTube

```csharp
SteamSettings.UGC.AddItemPreviewVideo(updateHandle, videoId);
```

### Commit the update

Once all fields have been updated you can commit the update with a change note.

```csharp
SteamSettings.UGC.SubmitItemUpdate(updateHandle, changeNote);
```
