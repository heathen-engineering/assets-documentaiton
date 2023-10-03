---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# UGC Query

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Designed to simplify the act of querying User Generated Content aka Workshop items from Steam this object can be used to create and manage queries.

The intended use is that a query will be created through one of the static Create methods to properly initialize the base query and you can then use simple calls on the object to modify the query, execute the query and step through query pages.

This is used by the [UGC Query Manager](../components/ugc-query-manager.md) which can its self simplify UGC query even further.

## Understanding UGC Queries

As with anything User Generated Content the process of querying records is done in stages. The raw API requires the following steps.

{% hint style="info" %}
Note our UGC Query tool simplifies this for you but understanding what is happening under the hood can be helpful when debugging.
{% endhint %}

### Handle

First we have to create a query handle, this is a pointer to a configuration that Valve will use when searching available UGC items. The handle is created as one of 3 types of query handles

* All Request\
  No base filter these types of queries return all manner of UGC items.\
  These queries use paging pulling back up to 50 at a time
* Details Request\
  These queries take file IDs in as part of the argument and do not using paging. They only return the items you directly ask for.
* User Request\
  These queries return items related to a given user such as a friend or your self

{% hint style="success" %}
You will notice Heathen's UGC Query doesn't ask you what type you want. We can infer what type is needed based on the arguments you pass in on the UgcQuery.Create method.
{% endhint %}

### Settings

Once you have a handle you can apply various settings to it. For example you can set the language, add tags to filter on, etc. The available settings can be accessed via the methods we describe below

* [SetLanguage](ugc-query.md#setlanguage)
* [SetMatchAnyTag](ugc-query.md#setmatchanytag)
* [SetRankedByTrandDays](ugc-query.md#setrankedbytrenddays)
* [SetReturnAdditionalPreviews](ugc-query.md#setreturnadditionalpreviews)
* [SetReturnChildren](ugc-query.md#setreturnchildren)
* [SetReturnKeyValueTags](ugc-query.md#setreturnkeyvaluetags)
* [SetReturnLongDescription](ugc-query.md#setreturnlongdescription)
* [SetReturnMetadata](ugc-query.md#setreturnmetadata)
* [SetReturnOnlyIDs](ugc-query.md#setreturnonlyids)
* [SetReturnPlaytimeStats](ugc-query.md#setreturnplaytimestats)
* [SetReturnTotalOnly](ugc-query.md#setreturntotalonly)
* [SetSearchText](ugc-query.md#setsearchtext)

### Execution

Finally once we have a handle and have configured it we need to execute the query. Note that query types `All` and `User` have pages so when you execute you may only receive a part of the total count. The [pageCount ](ugc-query.md#pagecount)field will tell you how many pages this query has once it has been executed at least once. You can set the page by simply setting the [Page ](ugc-query.md#page)field or by calling [SetPage](ugc-query.md#setpage). When the page is set the existing handle will be released and a new handle created.

### Release

{% hint style="success" %}
Note we release the handle for you at the end of each execution. \
\
This means you cannot execute the same query twice, but it also means that when you forget to dispose ... Heathen has you covered.\
\
What if you want/need to execute the same query twice?\
You need to rebuild the query to do that and you can do that easily by simply calling the "Create" method again or setting the page value, even if you set it to the same value it will rebuild the same query.
{% endhint %}

You should have noticed that the UgcQuery is a "Disposable" object. This means it needs to be cleaned up when your done with it and we made that easy to do. You could simply let the .NET garbage collector handle this but its advisable to call it your self&#x20;

`myQuery.Dispose();`

This will release any open handle insure all references are free.

## Definition

```csharp
public class UgcQuery : IDisposable
```

## Static Methods

We have created a number of Get methods you can use to quickly construct a UgcQuery to meet your needs.

### Get

#### General

```csharp
public static UgcQuery Get(EUGCQuery queryType, 
                           EUGCMatchingUGCType matchingType, 
                           AppId_t creatorApp, 
                           AppId_t consumerApp)
```

The first form of the Get method can be used with any type of query and simply gets a query ready for you to further modify.

#### Target Files

```csharp
public static UgcQuery Get(params PublishedFileId_t[] fileIds)
```

This form of the Get method takes one or more file IDs you would like to get more information on. This can be useful when already have a set of known file IDs such as the users subscribed IDs. You can also pass in a list or array of file IDs you would like to query.

#### Related to a given account or user

```csharp
public static UgcQuery Get(AccountID_t account, 
                           EUserUGCList listType, 
                           EUGCMatchingUGCType matchingType, 
                           EUserUGCListSortOrder sortOrder, 
                           AppId_t creatorApp, 
                           AppId_t consumerApp)
```

This option lets you create a query that looks for items related to a specific user or account.

### Get My Published

```csharp
public static UgcQuery GetMyPublished()
```

```csharp
public static UgcQuery GetMyPublished(AppData creatorApp, AppData consumerApp)
```

Creates a query to get all the published files related to the local user.

### Get Subscribed

```csharp
public static UgcQuery GetSubscribed()
```

The same as calling `Get(fileIds)` on the set of subscribed files the local user is subscribed to. This is the easiest way to get the details about all the workshop items this user is currently using.

### Get Played

```csharp
public static UgcQuery GetPlayed()
```

```csharp
public static UgcQuery GetPlayed(AppData creatorApp, AppData consumerApp)
```

Gets the set of workshop items the local player has played

## Fields and Attributes

### handle

```csharp
public UGCQueryHandle_t handle
```

The active query handle if any. This can be used to modify the query acter creating it. In most cases you wont need to use this directly.

### matchedRecordCount

```csharp
public uint matchedRecordCount
```

The number of matched records. This will be 0 untill the query is executed and should not be updated manually.

### pageCount

```csharp
public uint pageCount
```

The number of pages found for this query. This will be 0 until the query is exeucted and should not be updated manually.

### Page

```csharp
public uint Page { get; set; }
```

This indicates the current page the query is reading. Setting this value calls the [SetPage ](ugc-query.md#setpage)method.

### ResultList

```csharp
public List<UGCCommunityItem> ResultsList
```

This will be populated with the results when the query is executed ... assuming there are results to populate.

See [UGCCommunityItem ](workshop-item.md)for more info on how to use the items returned.

## Methods

### AddExcludedTag

```csharp
public bool AddExcludedTag(string tagName);
```

Adds a excluded tag to a pending UGC Query. This will only return UGC without the specified tag.

### AddRequiredKeyValueTag

```csharp
public bool AddRequiredKeyValueTag(string key, string value);
```

Adds a required key-value tag to a pending UGC Query. This will only return workshop items that have a key = pKey and a value = pValue.

### AddRequiredTag

```csharp
public bool AddRequiredTag(string tagName)
```

Adds a required tag to a pending UGC Query. This will only return UGC with the specified tag.

### SetAllowCachedResponce

```csharp
public bool SetAllowCachedResponse(uint maxAgeSeconds)
```

Set allow cached response from UGC Query

### SetCloudFileNameFilter

```csharp
public bool SetCloudFileNameFilter(string fileName)
```

Set the cloud file name filter value

### SetLanguage

```csharp
public bool SetLanguage(string language);
```

Sets the query item language

### SetMatchAnyTag

```csharp
public bool SetMatchAnyTag(bool anyTag)
```

Sets the query match any tag

### SetRankedByTrendDays

```csharp
public bool SetRankedByTrendDays(uint days);
```

Sets the query to rank by trend over the indicated days

### SetReturnAdditionalPreviews

```csharp
public bool SetReturnAdditionalPreviews(bool enable);
```

Should the query return additional previews or just the main

### SetReturnChildren

```csharp
public bool SetReturnChildren(bool enable);
```

Should the query return child items or just the main

### SetReturnKeyValueTags

```csharp
public bool SetReturnKeyValueTags(bool enable);
```

Should the query return key value tags

### SetReturnLongDescription

```csharp
public bool SetReturnLongDescription(bool enable);
```

Should the query return the long description of the item

### SetReturnMetadata

```csharp
public bool SetReturnMetadata(bool enable);
```

Should the query return metadata

### SetReturnOnlyIDs

```csharp
public bool SetReturnOnlyIDs(bool enable);
```

Should the query only return item IDs

### SetReturnPlaytimeStats

```csharp
public bool SetReturnPlaytimeStats(uint days);
```

Over what set of days should paly time stats be returned

### SetReturnTotalOnly

```csharp
public bool SetReturnTotalOnly(bool enable);
```

Should the query only return the matching count and not item data at all

### SetSearchText

```csharp
public bool SetSearchText(string text);
```

Sets the search text to be used by the query

### SetNextPage

```csharp
public bool SetNextPage();
```

Advances the active page forward by 1 if available

### SetPreviousPage

```csharp
public bool SetPreviousPage();
```

Steps back to the previous page if available

### SetPage

```csharp
public bool SetPage(uint page);
```

Sets the query to the indicated page

### Execute

```csharp
public bool Execute(UnityAction<UgcQuery> callback);
```

Executes the given query and registers a callback to catch its results

### ReleaseHandle

```csharp
public void ReleaseHandle();
```

Releases the query handle, this should be called when done with a query. This is automatically called when the object is disposed.

### Dispose

```csharp
public void Dispose();
```

Deconstructs the query and frees its handles
