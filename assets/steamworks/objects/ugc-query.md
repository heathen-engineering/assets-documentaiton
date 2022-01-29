# UGC Query

## Introduction

Designed to simplify the act of querying User Generated Content aka Workshop items from Steam this object can be used to create and manage queries.

The intended use is that a query will be created through one of the static Create methods to properly intialize the base query and you can then use simple calls on the object to modiy the query, execute the query and step through query pages.

This is used by the [UGC Query Manager](../components/ugc-query-manager.md) which can its self simplify UGC query even further.

## Definition

```csharp
public class UgcQuery
```

## Static Methods

These are inteded to be how you create a new UgcQuery object. Each creates a corisponding type of query.

### General Query

General use query common for example when browsing all available items

```csharp
public static UgcQuery Create(EUGCQuery queryType, 
                              EUGCMatchingUGCType matchingType, 
                              AppId_t creatorApp, 
                              AppId_t consumerApp)
```

* queryType\
  The type of query to run, see [EUGCQuery ](https://partner.steamgames.com/doc/api/ISteamUGC#EUGCQuery)for more details.
* matchingType\
  Used to specify the type of UGC queried for. See [EUGCMAtchingUGCType ](https://partner.steamgames.com/doc/api/ISteamUGC#EUGCMatchingUGCType)for more details.
* creatorApp\
  Filter by the app that created the item
* consumerApp\
  Filter by the app the item is created for

### File Query

Returns specific files back defined by ID. Use this to get the details on a set of published file IDs such as when returning the list of subscribed items

```csharp
public static UgcQuery Create(IEnumerable<PublishedFileId_t> fileIds);
```

* fileIds\
  The collection of IDs to search for

### User Query

Returns items relive to the given user account e.g. the favorited files or followed files

```csharp
public static UgcQuery Create(AccountID_t account, 
                              EUserUGCList listType, 
                              EUGCMatchingUGCType matchingType, 
                              EUserUGCListSortOrder sortOrder, 
                              AppId_t creatorApp, 
                              AppId_t consumerApp)
```

* account\
  This is the user account to search for
* listType\
  The type of list to return ... see [EUserUGCList ](https://partner.steamgames.com/doc/api/ISteamUGC#EUserUGCList)for more details
* matchingType\
  Used to specify the type of UGC queried for. See [EUGCMAtchingUGCType ](https://partner.steamgames.com/doc/api/ISteamUGC#EUGCMatchingUGCType)for more details.
* sortOrder\
  How should the results be sorted. See [EUserUGCListSortOrder ](https://partner.steamgames.com/doc/api/ISteamUGC#EUserUGCListSortOrder)for more details.
* creatorApp\
  Filter by the app that created the item
* consumerApp\
  Filter by the app the item is created for

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
public uint Page => get;
```

This indicates the current page the query is reading. Use the SetPage method to update this value and update the query for the desired page.

## Methods

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

### SEtReturnLongDescription

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

Advances the active page forward by 1 if avialable

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

Executes the given query and registeres a callback to catch its results

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
