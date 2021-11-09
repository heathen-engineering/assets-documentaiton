# UGC Query

## Introduction

Designed to simplify the act of querying User Generated Content aka Workshop items from Steam this object can be used to create and manage queries.

The intended use is that a query will be created through one of the static Create methods to properly intialize the base query and you can then use simple calls on the object to modiy the query, execute the query and step through query pages.

This is used by the [UGC Query Manager](../components/ugc-query-manager.md) which can its self simplify UGC query even further.

## Definition

```csharp
public class UgcQuery
```

### Static Methods

These are inteded to be how you create a new UgcQuery object. Each creates a corisponding type of query.

#### General Query

General use query common for example when browsing all available items

```csharp
public static UgcQuery Create(queryType, matchingType, creatorApp, consumerApp);
```

#### File Query

Returns specific files back defined by ID

```csharp
public static UgcQuery Create(fileIds);
```

#### User Query

Returns items relive to the given user account e.g. the favorited files or followed files

```csharp
public static UgcQuery Create(account, 
                              listType, 
                              matchingType, 
                              sortOrder,
                              creatorApp,
                              consumerApp);
```

### Fields and Attributes

| Type                  | Name               | Comment |
| --------------------- | ------------------ | ------- |
| UGCQueryHandle\_t     | handle             |         |
| uint                  | matchedRecordCount |         |
| uint                  | pageCount          |         |
| bool                  | isAllQuery         |         |
| bool                  | isUserQuery        |         |
| EUserUGClist          | listType           |         |
| EUGCQuery             | queryType          |         |
| EUGCMatchingUGCType   | matchingType       |         |
| EUserUGCListSortOrder | sortOrder          |         |
| AppId\_t              | creatorApp         |         |
| AppId\_t              | consumerApp        |         |
| AccountID\_t          | account            |         |
| uint                  | Page               |         |

### Methods

```csharp
public bool SetLanguage(language);
```

Sets the query item language

```csharp
public bool SetMatchhAnyTag(anyTag)
```

Sets the query match any tag

```csharp
public bool SetRankedByTrendDays(days);
```

Sets the query to rank by trend over the indicated days

```csharp
public bool SetReturnAdditionalPreviews(enable);
```

Should the query return additional previews or just the main

```csharp
public bool SetReturnChildren(enable);
```

Should the query return child items or just the main

```csharp
public bool SetReturnKeyValueTags(enable);
```

Should the query return key value tags

```csharp
public bool SetReturnLongDescription(enable);
```

Should the query return the long description of the item

```csharp
public bool SetReturnMetadata(enable);
```

Should the query return metadata

```csharp
public bool SetReturnOnlyIDs(enable);
```

Should the query only return item IDs

```csharp
public bool SetReturnPlaytimeStats(days);
```

Over what set of days should paly time stats be returned

```csharp
public bool SetReturnTotalOnly(enable);
```

Should the query only return the matching count and not item data at all

```csharp
public bool SetSearchText(text);
```

Sets the search text to be used by the query

```csharp
public bool SetNextPage();
```

Advances the active page forward by 1 if avialable

```csharp
public bool SetPreviousPage();
```

Steps back to the previous page if available

```csharp
public bool SetPage(page);
```

Sets the query to the indicated page

```csharp
public bool Execute(callback);
```

Executes the given query and registeres a callback to catch its results

```csharp
public void ReleaseHandle();
```

Releases the query handle, this should be called when done with a query. This is automatically called when the object is disposed.

```csharp
public void Dispose();
```

Deconstructs the query and frees its handles
