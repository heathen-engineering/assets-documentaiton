# UGC Query Manager

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

Search for and browse Steam Workshop items.

```csharp
public class UserGeneratedContentQueryManager : MonoBehaviour
```

## Definition

### Fields and Attributes

| Type                          | Name         | Comments                                        |
| ----------------------------- | ------------ | ----------------------------------------------- |
| AppId\_t                      | creatorAppId | The ID of the app that creates the items        |
| UserGeneratedContentItemQuery | activeQuerry | Settings to search for                          |
| int                           | CurrentFrom  | the index of the first item in the current list |
| int                           | CurrentTo    | the index of the last item in the current list  |
| int                           | TotalCount   | how many items are in the current query         |
| int                           | CurrentPage  | which page is currently loaded                  |



### Events

#### Results Returned

Occurs when the results are ready

#### Query Prepared

Occurs when the query is ready to return results

#### Results Updated

Occurs when the result list is updated

### Methods

```csharp
public void SearchAll(filter);
```

Search for all the items that match the input fiter.

```csharp
public void PrepareSearchAll(filter);
```

Prepares a search but doesn't execute it

```csharp
public void SearchFavorites(filter);
```

Search for favorited items that match the input filter.

```csharp
public void PrepareSearchFavorites(filter);
```

Prepares a search for favorited items that match the input filter but doens't execute it

```csharp
public void SearchFollowed(filter);
```

Search for followed items that match the input filter.

```csharp
public void PrepareSearchFollowed(filter);
```

Prepares a search for followed items that match the input filter but doens't execute it

```csharp
public void ExecuteSearch();
```

Executes a prepared search

```csharp
public void SetNextSearchPage();
```

Moves the page forward and executes the updated query

```csharp
public void SetPreviousSearchPage();
```

Moves the page back and executes the updated query

```csharp
public void SetSearchPage(page);
```

Sets a specific page and exuecutes the query
