# UGC Query Manager

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

Search for and browse Steam Workshop items.

```csharp
public class UserGeneratedContentQueryManager : MonoBehaviour
```

### Related Topics

#### Workshop Browser

{% embed url="https://kb.heathenengineering.com/assets/steamworks/learning/core-concepts/user-generated-content-workshop" %}

The UGC Workshop article includes a step by step guide on the use of UGC Query Manager to create an [In-Game Workshop browser](../../../../company/steam/steamworks/workshop/in-game-browser.md).

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
