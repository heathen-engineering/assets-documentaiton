# User Generated Content (Workshop)

## Introduction

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

The User Generate Content (UGC) API from Valve is used for a number of features including Leaderboard Details. This section of the Heathen Knowledge Base however deals with the use of UGC for Workshop files.

The typical use case is that you enable your users and or you yourself create workshop files (aka mods) and upload them to Valve's Workshop. These can then be browsed for and subscribed to by players. The system will then download the content that belongs to the subscribed mods and make that available to your game.

## Concepts

### Item File

This is not a single "file" such as a word.doc or folder.zip, instead this is an ID that represents a collection of content on the Steam UGC system and can be browsed for via the Steam Workshop interface. A given Workshop "file" may contain many files, it will have at least a description, name and preview image.

### Content Folder

When you create a new UGC item e.g. Workshop entry, you provide several bits of information including a "Content Folder Path". The files in this folder path will be collected by the Steam client, compressed and uploaded to Steam. You **should not** include compressed files such as zip or rar.&#x20;

### Subscription

As with DLC, Apps and Games, when Valve says you are "subscribed" to a thing it means that you have access to it. In the case of Workshop this means its been selected by the user and is or will be downloaded to the user's machine and keep up-to date.

### Browse the Workshop

While the typical use case is that the user would browse for items in the Steam Client, and this would be Heathen's recommendation as well, the Steam Client's UI is going to be duty built for the task where your game's UI is not.&#x20;

It is however possible to browse the workshop in game and Heathen's Steamworks SDK provides a number of tools to help you with this.

#### [UGC Query Manager](../../components/ugc-query-manager.md)

Heathen Engineering has created a componenet to simplify the task of searching and browsing Steam User Generacted Content items. This component can be used to create a query and cycle it over pages.

{% hint style="info" %}
Steam UGC Queries are page based queries that is Steam will return a subset of the matching records aka pages. To read all available records you would need ot iterate over all the avialable pages updating the query to match the requried page each time.
{% endhint %}

#### [UGC Query](../../objects/ugc-query.md)

The UGC Queryt Manager uses the UGC Query object to perform all of its actions. You can use these same tools to create a completely bespoke (custom) browser experience.&#x20;

## How To

### In Game Workshop Browser

{% hint style="info" %}
How you set up the UI is up to you, the [UGC Query Manager](../../components/ugc-query-manager.md) manages the query and its results for you, its up to you to display thouse to the user how you see fit.
{% endhint %}

#### Step 1

The first thing you will want to do is add a [UGC Query Manager](../../components/ugc-query-manager.md) to a game object related to your browser UI. This component provides the events your UI will listen on to update its display and the methods and values your UI will interact with to drive the query

#### Step 2

Create a UI controller that can listen on the Results Changed event of the UGC Query Manager and update your UI accodingly. That is write a new script to manage your brwoser UI and set it up such that it can listen on the [Results Upated](../../components/ugc-query-manager.md#events) event of the manager

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

The above assumes you have a reference to your [query manager](../../components/ugc-query-manager.md) in an attribute named `manager`&#x20;

result will be of type [UGC Read Community Item](../../objects/ugc-read-community-item.md) and contains all the details about that specific item.

Once defined you can refernce this in the Unity Inspector

![](<../../../../.gitbook/assets/image (173).png>)

#### Step 3

Next you will want to connect UI controls such as a Back and Next button up so the user can iterate over the query pages.

{% hint style="info" %}
Remimber UGC Query doesn't return all the results in one batch. You will be querying "page 1" which will return a subset of items. To fetch the next set e.g. "page 2" you need to incrament the Current Page vlaue of the manager.
{% endhint %}

![](<../../../../.gitbook/assets/image (160) (1).png>)

You should do the same for "Set Previous Search Page" so that the user can go back and forth. These methods are safe and will never step to a page that doesn't exist.

#### Step 4

Enabling search, you could do this in a few ways but the simplest is to trigger a search on the end edit of an InpuField ... this way when the user finished typing a search string and presses enter it will start the search.

That said it can be nice to have a Search Button that on click performed the searched using the text contained in the InputField ... the choice is up to you

![](<../../../../.gitbook/assets/image (172).png>)

Whatever your choice your UI should call the SearchAll method which takes a string as an input paramiters. That string is the filter string used by Valve to narrow results.
