# UGC Query Manager

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Search for and browse Steam Workshop items.

```csharp
public class UserGeneratedContentQueryManager : MonoBehaviour
```

### Related Topics

#### Workshop Browser

{% embed url="https://kb.heathenengineering.com/assets/steamworks/learning/core-concepts/user-generated-content-workshop" %}

The UGC Workshop article includes a step by step guide on the use of UGC Query Manager to create an [In-Game Workshop browser](../../guides/workshop/in-game-browser.md).

#### User Generated Content API

{% embed url="https://kb.heathenengineering.com/assets/steamworks/api/user-generated-content" %}

The User Generated Content API is the underlying tool set used by the query manager.

## Definition

## Fields and Attributes

| Type                          | Name         | Comments                                        |
| ----------------------------- | ------------ | ----------------------------------------------- |
| AppId\_t                      | creatorAppId | The ID of the app that creates the items        |
| UserGeneratedContentItemQuery | activeQuerry | Settings to search for                          |
| int                           | CurrentFrom  | the index of the first item in the current list |
| int                           | CurrentTo    | the index of the last item in the current list  |
| int                           | TotalCount   | how many items are in the current query         |
| int                           | CurrentPage  | which page is currently loaded                  |



## Events

### Results Returned

Occurs when the results are ready

### Query Prepared

Occurs when the query is ready to return results

### Results Updated

Occurs when the result list is updated

## Methods

### Search All

```csharp
public void SearchAll(filter);
```

Search for all the items that match the input fiter.

### Prepare Search All

```csharp
public void PrepareSearchAll(filter);
```

Prepares a search but doesn't execute it

### Search Favorites

```csharp
public void SearchFavorites(filter);
```

Search for favorited items that match the input filter.

### Prepare Search Favorites

```csharp
public void PrepareSearchFavorites(filter);
```

Prepares a search for favorited items that match the input filter but doens't execute it

### Search Followed

```csharp
public void SearchFollowed(filter);
```

Search for followed items that match the input filter.

### Prepare Search Followed

```csharp
public void PrepareSearchFollowed(filter);
```

Prepares a search for followed items that match the input filter but doens't execute it

### Execute Search

```csharp
public void ExecuteSearch();
```

Executes a prepared search

### Set Next Search Page

```csharp
public void SetNextSearchPage();
```

Moves the page forward and executes the updated query

### Set Previous Search Page

```csharp
public void SetPreviousSearchPage();
```

Moves the page back and executes the updated query

### Set Search Page

```csharp
public void SetSearchPage(page);
```

Sets a specific page and exuecutes the query
