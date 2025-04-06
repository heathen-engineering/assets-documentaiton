# In-Game Browser

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
How you set up the UI is up to you, the [UGC Query Manager](../../../../old-toolkit-for-steamworks/unity/objects/components/ugc-query-manager.md) manages the query and its results for you, its up to you to display those to the user how you see fit.
{% endhint %}

You can find a working example in the sample scenes names `7 Workshop Browser` this sample is designed to work with App 480 Spacewars and emulates the browser in Steam's Workshop UI.

## Set up

### Step 1

The first thing you will want to do is add a [UGC Query Manager](../../../../old-toolkit-for-steamworks/unity/objects/components/ugc-query-manager.md) to a game object related to your browser UI. This component provides the events your UI will listen on to update its display and the methods and values your UI will interact with to drive the query

### Step 2

Create a UI controller that can listen on the Results Changed event of the UGC Query Manager and update your UI accordingly. That is write a new script to manage your browser UI and set it up such that it can listen on the [Results Updated](../../../../old-toolkit-for-steamworks/unity/objects/components/ugc-query-manager.md#events) event of the manager

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

The above assumes you have a reference to your [query manager](../../../../old-toolkit-for-steamworks/unity/objects/components/ugc-query-manager.md) in an attribute named `manager`&#x20;

result will be of type [UGC Read Community Item](../../../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item.md) and contains all the details about that specific item.

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
