---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# UserGeneratedContent.Client

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

```csharp
using UGCClient= HeathenEngineering.SteamworksIntegration.API.UserGeneratedContent.Client;
```

```csharp
public static class UserGeneratedContent.Client
```

## Events

### EventItemDownloaded

Occurs when a UGC item is downloaded

```csharp
public static WorkshopDownloadedItemResultEvent EventItemDownloaded;
```

The event handler would look similar to&#x20;

```csharp
void HandleEvent(DownloadItemResult_t arg0)
{
    //Do Work
}
```

### EventWorkshopItemInstalled

Called when a workshop item has been installed or updated

```csharp
public static WorkshopItemInstalledEvent EventWorkshopItemInstalled;
```

The event handler would look similar to&#x20;

```csharp
void HandleEvent(ItemInstalled_t arg0)
{
    //Do Work
}
```

## Methods

### AddAppDependency

```csharp
public static void AddAppDependency(PublishedFileId_t fileId, 
                                    AppId_t appId, 
                                    Action<AddAppDependencyResult_t, bool> callback)
```

The callback for this method would look like the following.

{% hint style="info" %}
This is a native callback, details as to the meaning of fields in the AddAppDependencyResult\_t object can be found [here](https://partner.steamgames.com/doc/api/ISteamUGC#AddAppDependencyResult\_t).
{% endhint %}

```csharp
void Callback(AddAppDependencyResult_t responce, bool ioError)
{
    // Do Work
}
```

Adds a dependency between the given item and the appid. This list of dependencies can be retrieved by calling GetAppDependencies. This is a soft-dependency that is displayed on the web. It is up to the application to determine whether the item can actually be used or not.

### AddDependency

```csharp
public static void AddDependency(PublishedFileId_t parentFileId, 
                                PublishedFileId_t childFileId, 
                                Action<AddUGCDependencyResult_t, bool> callback)
```

{% hint style="info" %}
This is a native callback, details as to the meaning of fields in the AddUGCDependencyResult\_t object can be found [here](https://partner.steamgames.com/doc/api/ISteamUGC#AddUGCDependencyResult\_t).
{% endhint %}

```csharp
void Callback(AddUGCDependencyResult_t responce, bool ioError)
{
    // Do Work
}
```

Adds a workshop item as a dependency to the specified item. If the nParentPublishedFileID item is of type k\_EWorkshopFileTypeCollection, than the nChildPublishedFileID is simply added to that collection. Otherwise, the dependency is a soft one that is displayed on the web and can be retrieved via the ISteamUGC API using a combination of the m\_unNumChildren member variable of the SteamUGCDetails\_t struct and GetQueryUGCChildren.

### AddExcludedTag

```csharp
public static bool AddExcludedTag(UGCQueryHandle_t handle, string tagName)
```

Adds a excluded tag to a pending UGC Query. This will only return UGC without the specified tag.

### AddItemKeyValueTag

```csharp
public static bool AddItemKeyValueTag(UGCUpdateHandle_t handle, 
                                string key, string value)
```

Adds a key-value tag pair to an item. Keys can map to multiple different values (1-to-many relationship). Key names are restricted to alpha-numeric characters and the '\_' character. Both keys and values cannot exceed 255 characters in length. Key-value tags are searchable by exact match only.

### AddItemPreviewFile

```csharp
public static bool AddItemPreviewFile(UGCUpdateHandle_t handle, 
                                string previewFile, EItemPreviewType type)
```

Adds an additional preview file for the item. Then the format of the image should be one that both the web and the application(if necessary) can render, and must be under 1MB.Suggested formats include JPG, PNG and GIF.

### AddItemPreviewVideo

```csharp
public static bool AddItemPreviewVideo(UGCUpdateHandle_t handle, string videoId)
```

Adds an additional video preview from YouTube for the item.

### AddItemToFavorites

```csharp
public static void AddItemToFavorites(AppId_t appId, 
                PublishedFileId_t fileId, 
                Action<UserFavoriteItemsListChanged_t, bool> callback)
```

Adds workshop item to the users favorite list. The callback to this method would look like the following

{% hint style="info" %}
This is a native Steam API callback you can find more details [here](https://partner.steamgames.com/doc/api/ISteamUGC#UserFavoriteItemsListChanged\_t).
{% endhint %}

```csharp
void Callback(UserFavoriteItemsListChanged_t responce, bool ioError)
{
    // Do Work
}
```

### AddRequiredKeyValueTag

```csharp
public static bool AddRequiredKeyValueTag(UGCQueryHandle_t handle, 
                                string key, string value)
```

Adds a required key-value tag to a pending UGC Query. This will only return workshop items that have a key = pKey and a value = pValue.

### AddRequiredTag

```csharp
public static bool AddRequiredTag(UGCQueryHandle_t handle, string tagName)
```

Adds a required tag to a pending UGC Query. This will only return UGC with the specified tag.

### CreateItem

```csharp
public static bool CreateItem(WorkshopItemData item, 
                              WorkshopItemPreviewFile[] additionalPreviews, 
                              string[] additionalYouTubeIds, 
                              WorkshopItemKeyValueTag[] additionalKeyValueTags, 
                              Action<WorkshopItemDataCreateStatus> callback = null)
```

The first overload handles the creation and update of new items in a single line call.&#x20;

The first parameter defines the core fields of the item to be created, note the [WorkshopItemData.Create](../data-layer/workshop-item-data.md) method simply calls this overload.

The remaining parameters deal with additional preview images and videos as well as the key value tag system

The callback for this overload would look similar to following.

{% hint style="info" %}
See the [WorkshopItemDataCreateStatus](../objects/workshop-item-data-create-status.md) definition for more information on what fields it contains.
{% endhint %}

```csharp
void Callback(WorkshopItemDataCreateStatus status)
{
    //Do Work
}
```

The second overload is only creates an empty UGC File. You would then manually start the update process and set each of its fields. This approach is more akin to using the Raw Steam API.

{% hint style="info" %}
Learn more about manual creation and update of items [here](usergeneratedcontent.client.md#create-and-update-items).
{% endhint %}

```csharp
public static void CreateItem(AppId_t appId, EWorkshopFileType type, 
                Action<CreateItemResult_t, bool> callback)
```

The callback for this overload would look similar to the following.

```csharp
void Callback(CreateItemResult_t responce, bool ioError)
{
    // Do Work
}
```

This works exsactly the same as the native Steam API callback as documented [here](https://partner.steamgames.com/doc/api/ISteamUGC#CreateItemResult\_t) and uses those native Steam API structures.

### CreateQueryAllRequest

```csharp
public static UGCQueryHandle_t CreateQueryAllRequest(EUGCQuery queryType, 
                                EUGCMatchingUGCType matchingFileType, 
                                AppId_t creatorAppId, 
                                AppId_t consumerAppId, 
                                uint page)
```

{% hint style="info" %}
The [UGC Query Manager](../components/ugc-query-manager.md) can make working with quires much simpler.
{% endhint %}

Query for all matching UGC. You can use this to list all of the available UGC for your app. You must release the handle returned by this function by calling WorkshopReleaseQueryRequest when you are done with it!

### CreateQueryDetailsRequest

All of the overloads do the same thing they simply reduce the need for in line conversion when using different types of collecitons.

```csharp
public static UGCQueryHandle_t CreateQueryDetailsRequest(
                PublishedFileId_t[] fileIds)
```

```csharp
public static UGCQueryHandle_t CreateQueryDetailsRequest(
                List<PublishedFileId_t> fileIds)
```

```csharp
public static UGCQueryHandle_t CreateQueryDetailsRequest(
                IEnumerable<PublishedFileId_t> fileIds)
```

{% hint style="info" %}
The [UGC Query Manager](../components/ugc-query-manager.md) can make working with quires much simpler.
{% endhint %}

Query for the details of specific workshop items. You must release the handle returned by this function by calling WorkshopReleaseQueryRequest when you are done with it!

### CreateQueryUserRequest

```csharp
public static UGCQueryHandle_t CreateQueryUserRequest(
                                AccountID_t accountId, 
                                EUserUGCList listType, 
                                EUGCMatchingUGCType matchingType, 
                                EUserUGCListSortOrder sortOrder, 
                                AppId_t creatorAppId, 
                                AppId_t consumerAppId, 
                                uint page)
```

Query UGC associated with a user. You can use this to list the UGC the user is subscribed to amongst other things. You must release the handle returned by this function by calling WorkshopReleaseQueryRequest when you are done with it!

### ReleaseQueryRequest

```csharp
public static bool ReleaseQueryRequest(UGCQueryHandle_t handle)
```

Frees a UGC query

### DeleteItem

```csharp
public static void DeleteItem(PublishedFileId_t fileId, 
                                Action<DeleteItemResult_t, bool> callback)
```

Requests delete of a UGC item

{% hint style="info" %}
This is a native callback you can find more details on it [here](https://partner.steamgames.com/doc/api/ISteamUGC#DeleteItemResult\_t).
{% endhint %}

```csharp
void Callback(DeleteItemResult_t responce, bool ioFailure)
{
    //Do Work
}
```

### DownloadItem

```csharp
public static bool DownloadItem(PublishedFileId_t fileId, bool setHighPriority)
```

Request download of a UGC item

### GetAppDependencies

```csharp
public static void GetAppDependencies(PublishedFileId_t fileId, 
                   Action<GetAppDependenciesResult_t, bool> callback)
```

Request the app dependencies of a UGC item

### GetItemDownloadInfo

```csharp
public static bool GetItemDownloadInfo(PublishedFileId_t fileId, 
                   out float completion)
```

Request the download informaiton of a UGC item

### GetItemInstallInfo

```csharp
public static bool GetItemInstallInfo(PublishedFileId_t fileId, 
                                out ulong sizeOnDisk, 
                                out string folderPath, 
                                out DateTime timeStamp)
```

Request the installation informaiton of a UGC item

### GetItemInstallInfo

```csharp
public static bool GetItemInstallInfo(PublishedFileId_t fileId, 
                                out ulong sizeOnDisk, 
                                out string folderPath, 
                                uint folderSize, 
                                out DateTime timeStamp)
```

Request the installation informaiton of a UGC item

### GetItemState

```csharp
public static EItemState GetItemState(PublishedFileId_t fileId)
```

Gets the current state of a workshop item on this client.

### ItemStateHasFlag

```csharp
public static bool ItemStateHasFlag(EItemState value, EItemState checkflag)
```

Checks if the 'checkFlag' value is in the 'value'

### ItemStateHasAllFlags

```csharp
public static bool ItemStateHasAllFlags(EItemState value, 
                                params EItemState[] checkflags)
```

Cheks if any of the 'checkflags' values are in the 'value'

### GetItemUpdateProgress

```csharp
public static EItemUpdateStatus GetItemUpdateProgress(UGCUpdateHandle_t handle, 
                                out float completion)
```

Gets the progress of an item update.

### GetNumSubscribedItems

```csharp
public static uint GetNumSubscribedItems()
```

Returns the number of subscribed UGC items

### GetQueryAdditionalPreview

```csharp
public static bool GetQueryAdditionalPreview(UGCQueryHandle_t handle, 
                                uint index, 
                                uint previewIndex, 
                                out string urlOrVideoId, 
                                uint urlOrVideoSize, 
                                string fileName, 
                                uint fileNameSize, 
                                out EItemPreviewType type)
```

Request an additional preview for a UGC item

### GetQueryChildren

```csharp
public static bool GetQueryChildren(UGCQueryHandle_t handle, 
                                uint index, 
                                PublishedFileId_t[] fileIds, 
                                uint maxEntries)
```

Request the child items of a given UGC item

### GetQueryKeyValueTag

```csharp
public static bool GetQueryKeyValueTag(UGCQueryHandle_t handle, 
                                uint index, 
                                uint keyValueTagIndex, 
                                out string key, 
                                string value)
```

Retrieve the details of a key-value tag associated with an individual workshop item after receiving a querying UGC call result.

### GetQueryMetadata

```csharp
public static bool GetQueryMetadata(UGCQueryHandle_t handle, 
                                uint index, 
                                out string metadata, 
                                uint size)
```

Request the metadata of a UGC item

### GetQueryNumAdditionalPreviews

```csharp
public static uint GetQueryNumAdditionalPreviews(UGCQueryHandle_t handle, 
                                uint index)
```

Request the number of previews of a UGC item

### GetQueryNumKValueTags

```csharp
public static uint GetQueryNumKeyValueTags(UGCQueryHandle_t handle, uint index)
```

Request the number of key value tags for a UGC item

### GetQuyPreviewURL

```csharp
public static bool GetQueryPreviewURL(UGCQueryHandle_t handle, 
                uint index, 
                out string URL, 
                uint urlSize)
```

Get the preview URL of a UGC item

### GetQueryResults

```csharp
public static bool GetQueryResult(UGCQueryHandle_t handle, 
                uint index, 
                out SteamUGCDetails_t details)
```

Fetch the results of a UGC query

### GetQueryStatistic

```csharp
public static bool GetQueryStatistic(UGCQueryHandle_t handle, 
                uint index, 
                EItemStatistic statType, 
                out ulong statValue)
```

Fetch the statistics of a UGC query

### GetSubscribedItems

```csharp
public static uint GetSubscribedItems(PublishedFileId_t[] fileIDs, 
                uint maxEntries)
```

Get the file IDs of all subscribed UGC items up to the array size. This is a wrapper around the raw API entry and maintained for backward compatibility.

or

```csharp
public static PublishedFileId_t[] GetSubscribedItems()
```

Returns the list of items the user is subscribed to as a simple array.

or

```csharp
public static void GetSubscribedItems(Action<List<UGCCommunityItem>> callback)
```

This will query for the details of the items the user is subscribed to and invoke a callback when those details are returned.

### GetUserItemVote

```csharp
public static void GetUserItemVote(PublishedFileId_t fileId, 
                Action<GetUserItemVoteResult_t, bool> callback)
```

Get the item vote value of a UGC item. The callback for this would look like the following

```csharp
void Callback(GetUserItemVoteResult_t responce, bool ioFailure)
{
    // Do Work
}
```

### GetWorkshopEULAStatus

```csharp
public static void GetWorkshopEULAStatus(
                Action<WorkshopEULAStatus_t, bool> callback)
```

Asynchronously retrieves data about whether the user accepted the Workshop EULA for the current app. The callback for this method would look like the following.

```csharp
void Callback(WorkshoEULAStatus_t responce, bool ioFailure)
{
    // Do Work
}
```

### ShowWorkshopEULA

```csharp
public static bool ShowWorkshopEULA()
```

Show the app's latest Workshop EULA to the user in an overlay window, where they can accept it or not

### RemoveAppDependency

```csharp
public static void RemoveAppDependency(PublishedFileId_t fileId, 
                AppId_t appId, 
                Action<RemoveAppDependencyResult_t, bool> callback)
```

Request the removal of app dependency from a UGC item

### RemoveDependency

```csharp
public static void RemoveDependency(PublishedFileId_t parentFileId, 
                PublishedFileId_t childFileId, 
                Action<RemoveUGCDependencyResult_t, bool> callback)
```

Request the removal of a dependency from a UGC item

### RemoveItemFromFavorites

```csharp
public static void RemoveItemFromFavorites(AppId_t appId, 
                PublishedFileId_t fileId, 
                Action<UserFavoriteItemsListChanged_t, bool> callback)
```

Request the item be removed from the user's favourites list if present

### RemoveItemKeyValueTags

```csharp
public static bool RemoveItemKeyValueTags(UGCUpdateHandle_t handle, string key)
```

Remove UGC Item key value tags

### RemoveItemPreview

```csharp
public static bool RemoveItemPreview(UGCUpdateHandle_t handle, uint index)
```

Remove UGC Item Preview&#x20;

### RequestDetails

```csharp
public static void RequestDetails(PublishedFileId_t fileId, 
        uint maxAgeSeconds, 
        Action<SteamUGCRequestUGCDetailsResult_t, bool> callback)
```

Request details of a given UGC item

### SendQueryUGCRequest

```csharp
public static void SendQueryUGCRequest(UGCQueryHandle_t handle, 
                Action<SteamUGCQueryCompleted_t, bool> callback)
```

Send a UGC query for processing

### SetAllowCashedResponse

```csharp
public static bool SetAllowCachedResponse(UGCQueryHandle_t handle, 
                uint maxAgeSeconds)
```

Set the allow cashed response on Steam

### SetCloudFileNameFilter

```csharp
public static bool SetCloudFileNameFilter(UGCQueryHandle_t handle, 
                string fileName)
```

Set the file name filter value for use with queries

### SetItemContent

```csharp
```

Sets the folder path that Valve will upload from when submitting an item update

### SetItemDescription

```csharp
```

Sets the item description of the item when submitting an item update

### SetItemMetadata

```csharp
```

Sets the item metadata of the item when submitting an item update

### SetItemPreview

### SetItemTags

### SetItemTitle

### SetItemUpdateLanguage

### SetItemVisibility

### SetLanguage

### SetMatchAnyTag

### SetRankedByTrendDays

### SetReturnAdditionalPreviews

### SetReturnChildren

### SetReturnKeyalueTags

### SetReturnLongDescription

### SetReturnMetadata

### SetReturnOnlyIDs

### SetReturnPlaytimeStats

```csharp
public static bool SetReturnPlaytimeStats(UGCQueryHandle_t handle, uint days)
```

Set a query to return the playtime stats for related items

### SetReturnTotalOnly

```csharp
public static bool SetReturnTotalOnly(UGCQueryHandle_t handle, bool totalOnly)
```

Set a query to only return the total number of files that match the arguments

### SetSearchText

```csharp
public static bool SetSearchText(UGCQueryHandle_t handle, string text)
```

Sets the search text used when executing a UGC query

### SetUserItemVote

```csharp
public static void SetUserItemVote(PublishedFileId_t fileID, 
                bool voteUp, 
                Action<SetUserItemVoteResult_t, bool> callback)
```

Sets the vote value for a given item from this user.

### StartItemUpdate

```csharp
public static UGCUpdateHandle_t StartItemUpdate(AppId_t appId, 
                PublishedFileId_t fileID)
```

Request the start of an item update. This must be called before you set item preview, description, etc.

### StartPlaytimeTracking

```csharp
public static void StartPlaytimeTracking(PublishedFileId_t[] fileIds, 
                Action<StartPlaytimeTrackingResult_t, bool> callback)
```

Start tracking playtime for the indicated items.

### StopPlaytimeTracking

```csharp
public static void StopPlaytimeTracking(PublishedFileId_t[] fileIds, 
                Action<StopPlaytimeTrackingResult_t, bool> callback)
```

Stop tracking playtime for the indicated items.

### StopPlaytimeTrackingForAllItems

```csharp
public static void StopPlaytimeTrackingForAllItems(
                Action<StopPlaytimeTrackingResult_t, bool> callback)
```

Stop tracking playtime for all relevant items

### SubmitItemUpdate

```csharp
public static void SubmitItemUpdate(UGCUpdateHandle_t handle, 
                string changeNote, 
                Action<SubmitItemUpdateResult_t, bool> callback)
```

Submit an update request committing any changes made since the StartItemUpdate request.

### SubscribeItem

```csharp
public static void SubscribeItem(PublishedFileId_t fileId, 
        Action<RemoteStorageSubscribePublishedFileResult_t, bool> callback)
```

Subscribe to the indicated item

### SuspendDownloads

```csharp
public static void SuspendDownloads(bool suspend)
```

Suspend downloads

### UnsubscribeItem

```csharp
public static void UnsubscribeItem(PublishedFileId_t fileId, 
        Action<RemoteStorageUnsubscribePublishedFileResult_t, bool> callback)
```

Unsubscribe to the indicated item

### UpdateItemPreviewFile

```csharp
public static bool UpdateItemPreviewFile(UGCUpdateHandle_t handle, 
                uint index, 
                string file)
```

Update item preview image file

### UpdateItemPreviewVideo

```csharp
public static bool UpdateItemPreviewVideo(UGCUpdateHandle_t handle, 
                uint index, 
                string videoId)
```

Update item preview video

## How To

### Create and Update Items

Creating a new item can be done in one of two ways.

#### One liner

```csharp
UGC.CreateItem(itemdata, callback);
```

When using the 1 liner approach you will first create a [Workshop Item Data](../data-layer/workshop-item-data.md) object. This object defines the item you wish to create e.g. its name, description, content folder, etc.

The callback for this method is a delegate that takes 1 parameter of type [Workshop Item Data Create Status](../objects/workshop-item-data-create-status.md).

Example:

Assuming a method such as

```csharp
public void Foo(WorkshopItemDataCreateStats status)
{
    if(!status.hasError)
        //Do Work
    else
        //Something bad happened
}
```

Then you can call the method such as

```csharp
UGC.CreateItem(itemdata, Foo);
```

To learn more about [callbacks](../../../guides/development/callbacks.md) please read the related article.

The status returned to the callback will indicate the status of the operation. Note that the operation occurs in two stages. First a blank item is created and then once that has been found successful that blank item will be updated with the content and settings indicated thus it is possible for a blank item to be created but for the update to fail. Please see the [results](../objects/workshop-item-data-create-status.md#createitemresult) in the status object for more details.

#### Step by step

```csharp
UGC.CreateItem(appId, callback);
```

This callback will contain a UGCUpdateHandle\_t which can be used by other methods to update key features using the following methods

You can also use these tools to modify and existing file assuming you are its author

```csharp
UGC.StartItemUpdate(appId, fileId);
```

* AddItemKeyValueTag
* AddItemPreviewFile
* AddItemPreviewVideo
* SetItemContent
* SetItemDescription
* SetItemMetadata
* SetItemPreview
* SetItemTags
* SetItemTitle
* SetItemUpdateLanguage
* SetItemVisibility
* UpdateItemPreviewVideo
* UpdateItemPreviewFIle
* UpdateItemPreviewVideo
* RemoveItemKeyValueTags
* RemoveItemPreview

For example the following code would update the title and description

```csharp
UGC.SetItemTitle(updateHandle, "title");
UGC.SetItemDescription(updatehandle, "description");
```

When complete you should submit the update

```csharp
UGC.SubmitItemUpdate(handle, changenote, callback);
```

### Browse Items

The easiest way to handle a UGC / Workshop browser in game is to use the [UGC Query Manager](../components/ugc-query-manager.md). The manager uses the same features present in the interface so it can be done manually.

The remainder of this section talks about manually querying items.

The process is similar in that you would "create" or "start" a query which will give you a `UGCQueryHandle_t` which can then be modified to fine tune your query before submitting it to get the matching records.

To crete the `UGCQueryHandle_t`

```csharp
//Query all UGC for a particular App ID
var handle = UGC.CreateQueryAllRequest(type,
                                       fileType,
                                       creatAppId,
                                       consumeAppId,
                                       page);
                                                                
// or
//Query for specific files by file ID
var handle = UGC.CreateQueryDetailRequest(files);

//or
//Query for files related to a specific user
var handle = UGC.CreateQueryUserRequest(account,
                                        listType,
                                        matchType,
                                        sortOrder,
                                        createAppId,
                                        consumeAppId,
                                        page);
```

Once you have created your handle you can modify the way it searches for matching items by calling the following methods.

* AddExcludeTag
* AddRequiredKeyValueTag
* AddRequiredTag
* SetAllowCashedResponse
* SetCloudFileNameFilter
* SetLanguage
* SetMatchAnyTag
* SetRankedByTrendDays
* SetReturnAdditionalPreviews
* SetReturnChildren
* SetReturnKeyValueTags
* SetReturnLongDescription
* SetReturnMetadata
* SetReturnOnlyIDs
* SetReturnPlaytimeStats
* SetReturnTotalOnly
* SetSearchText

Once you have your query set up you can submit it to fetch the related items. Note the UGC Query system is a page query system. It will never return more than 50 items (determined by Valve) and so you will need to increment the page in your query handle to fetch each successive set of records.&#x20;

You can see how we implemented paging in the [UGC Query Manager](../components/ugc-query-manager.md) if you wished to do so your self or simply to better understand the system.

```csharp
//When ready send the query so Valve can process it
UGC.SendQueryUGCRequest(handle, callback);
```

When the callback is invoked its parameter will indicate the result state and query handle, assuming the state is eResultOk you can fetch the found items via, the following assumes `param` is the SteamUGCQueryComplete\_t object returned by the SendQueryUGCRequest's callback

```csharp
//If nothing went wrong
if(param.m_eResult == EResult.k_EResultOK)
{
    //Get the total records found
    var totalResults = param.m_unTotalMatchingResutls;
    
    //Get the number of pages involved
    var pageCount = (uint)MathF.Clamp((int)matchedRecordCount / 50, 1, int.MaxValue);
    if(pageCount * 50 < matchedRecordCount)
        pageCount++;
    
    //Get the number of results in this run/page
    var returned = param.m_unNumResultsReturned;
    
    for(int i=0; i < returned; i++)
    {
        UGC.GetQueryResult(param.m_handle, 
                           (uint)i,
                           out SteamUGCDetails_t detail);
        
        //detail now contains all of the data for this item, do with it what you will
    }
    
    //We must release the handle when done reading it
    UGC.ReleaseQueryRequest(param.m_handle);
}
```

Getting the next page of data is done the same way, you will need to track what page your on and howmany there are and create a new query updating the page.

Our UGC Query Manager does this fore you. You can simply incrament the page by calling `SetPage` and we will release any existing handle and fetch a new handle for the next page. You will need to re apply any modifications to the query you may have done before executing it again.&#x20;

### Get Subscribed Items

To get the list of subscirbed items e.g. items the user has indicated should be installed

```csharp
var results = UGC.GetSubscribedItems();
```

