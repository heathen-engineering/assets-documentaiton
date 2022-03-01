# UserGeneratedContent.Client

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

```csharp
using UGCClient= HeathenEngineering.SteamworksIntegraiton.API.UserGeneratedContent.Client;
```

```csharp
public static class UserGeneratedContent.Client
```

### What can it do?

Create, download, browse and edit Steam UGC files aka Steam Workshop.

### Related Components

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/ugc-query-manager" %}

### Related Obejcts

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/ugc-query-manager" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/ugc-query" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/ugc-read-community-item" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/workshop-item-data" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/workshop-item-data-create-status" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/workshop-item-key-value-tag" %}

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/workshop-item-preview-file" %}

## Events

### Item Downloaded

Occurs when a UGC item is downloaded

### Workshop Item Installed

Called when a workshop item has been installed or updated

## How To

### Create and Update Items

Creating a new item can be done in one of two ways.

#### One liner

```csharp
UGC.CreateItem(itemdata, callback);
```

When using the 1 liner approach you will first create a [Workshop Item Data](../objects/workshop-item-data.md) object. This object defines the item you wish to create e.g. its name, description, content folder, etc.

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

To learn more about [callbacks](../../../company/concepts/callbacks.md) please read the related article.

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

