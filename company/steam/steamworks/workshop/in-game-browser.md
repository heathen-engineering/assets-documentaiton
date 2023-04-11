# In-Game Browser

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../">Guides and Tutorials</a></td><td><a href="../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../assets/physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../assets/ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% hint style="info" %}
How you set up the UI is up to you, the [UGC Query Manager](../../../../assets/steamworks/unity/components/ugc-query-manager.md) manages the query and its results for you, its up to you to display those to the user how you see fit.
{% endhint %}

You can find a working example in the sample scenes names `7 Workshop Browser` this sample is designed to work with App 480 Spacewars and emulates the browser in Steam's Workshop UI.

## Set up

### Step 1

The first thing you will want to do is add a [UGC Query Manager](../../../../assets/steamworks/unity/components/ugc-query-manager.md) to a game object related to your browser UI. This component provides the events your UI will listen on to update its display and the methods and values your UI will interact with to drive the query

### Step 2

Create a UI controller that can listen on the Results Changed event of the UGC Query Manager and update your UI accordingly. That is write a new script to manage your browser UI and set it up such that it can listen on the [Results Updated](../../../../assets/steamworks/unity/components/ugc-query-manager.md#events) event of the manager

PSEDO CODE EXAMPLE

```csharp
public void HandleResultsChanged()
{
    foreach(var result in manager.activeQuery.ResultsList)
    {
        // Instantate a new record
        // set its values based on the data present in result
    }
}
```

The above assumes you have a reference to your [query manager](../../../../assets/steamworks/unity/components/ugc-query-manager.md) in an attribute named `manager`&#x20;

result will be of type [UGC Read Community Item](../../../../assets/steamworks/objects/ugc-community-item.md) and contains all the details about that specific item.

Once defined you can reference this in the Unity Inspector

![](<../../../../.gitbook/assets/image (173) (1).png>)

### Step 3

Next you will want to connect UI controls such as a Back and Next button up so the user can iterate over the query pages.

{% hint style="info" %}
Remember UGC Query doesn't return all the results in one batch. You will be querying "page 1" which will return a subset of items. To fetch the next set e.g. "page 2" you need to increment the Current Page value of the manager.
{% endhint %}

![](<../../../../.gitbook/assets/image (160) (1) (1) (1).png>)

You should do the same for "Set Previous Search Page" so that the user can go back and forth. These methods are safe and will never step to a page that doesn't exist.

### Step 4

Enabling search, you could do this in a few ways but the simplest is to trigger a search on the end edit of an InputField, this way when the user finished typing a search string and presses enter it will start the search.

That said it can be nice to have a Search Button that on click performed the searched using the text contained in the InputField. The choice is up to you

![](<../../../../.gitbook/assets/image (172) (1) (1) (1).png>)

Whatever your choice your UI should call the SearchAll method which takes a string as an input parameters. That string is the filter string used by Valve to narrow results.
