# Workshop

{% embed url="https://partner.steamgames.com/doc/features/workshop" %}

> The Steam Workshop is designed as a place for your fans and community members to participate in the creation of content for your game. The form of this creation by community members can vary depending on the nature of the game and what kind of control you wish to have over the content in your game.

There are steps you need to take in the Steam Developer Portal to enable Steam Workshop for your game. Be sure you have read Valve's implementation guide and followed its instructions.

{% embed url="https://partner.steamgames.com/doc/features/workshop/implementation#EnableISteamUGC" %}

The following is a snip-it from the above-linked document. Be sure you do read the original document first; this is here as a quick reference only.

## Enabling UGC for a Game or Application

Before workshop items can be uploaded to the Steamworks backend, two configuration settings must be made: Configuring Steam Cloud Quotas and Enabling the UGC API.\
\
The Steam Cloud feature is used to store the preview images associated with workshop items. The Steam Cloud Quota can be configured with the following steps:\


1. Navigate to the [Steam Cloud Settings](https://partner.steamgames.com/apps/cloud/) page in the App Admin panel.
2. Set the **Byte quota per user** and the **Number of files allowed per user** to appropriate values for preview image storage
3. Click Save
4. From the **Publish** tab, click **Prepare for Publishing**
5. Click **Publish to Steam** and complete the process to publish the change.

\
Enabling the UGC API can be accomplished with the following steps:\


1. You can just navigate to the [Steam Workshop Configuration](https://partner.steamgames.com/apps/workshop/) page in the App Admin panel.
2. Find the **Additional Configuration Options** section.
3. Check **Enable ISteamUGC for file transfer**.
4. Click **Save**.
5. From the **Publish** tab, click **Prepare for Publishing**.
6. Click **Publish to Steam** and complete the process to publish the change.

Once these settings are in place, workshop content can be uploaded via the API.

## Working with UGC

<figure><img src="../.gitbook/assets/image (382).png" alt="Image for reference find the original at https://partner.steamgames.com/doc/features/workshop/implementation#CreateUploadContent"><figcaption><p>Image for reference only, find the original at <a href="https://partner.steamgames.com/doc/features/workshop/implementation#CreateUploadContent">https://partner.steamgames.com/doc/features/workshop/implementation#CreateUploadContent</a></p></figcaption></figure>

The process of uploading content to UGC is a simple 2-step process.

### Create an Item

Using our tools, you will create a new empty item; this will provide you with a Published File handle that can be used in the second step.

### Updating an Item

This process lets you update an existing Published File. You do this by calling "Start Update", which provides you with an update handle. You can then set each field of the item, such as Name, Description, Preview Image, and so on, and finalise the update with Submit item update.

## Examples

### Create Item

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Workshop Item Editor to power in-game Workshop tools..

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

The base editor defines the minimal required fields which can be connected to Input Fields for user or code-based population.

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

Add the Create & Update settings to expand with optional data, use the Create New or Create and Update functions to submit the item to Steam.

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

Add the Events settings to expose key events to help drive your editor UI&#x20;

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
// Use the Workshop Item Editor Data to build up your item
WorkshopItemEditorData data = new();
data.title = "New Item";
data.description = "My first workshop item";
data.content = new("C:\\MyModContent");
data.preview = new("C:\\MyModPreviewImage.png");
data.visibility = ERemoteStoragePublishedFileVisibility.k_ERemoteStoragePublishedFileVisibilityPrivate;

// Now you can create and update the item
// each callback is optional, but you should at least
// use HandleCompletion
data.Create(HandleCompletion, HandleUpdateStarted, HandleNewItemCreated);

public void HandleNewItemCreated(CreateItemResult createResult)
{
    // Invoked after the new file ID has been created, but before it
    // has had all its values set
}

public void HandleUpdateStarted(UGCUpdateHandle_t updateHandle)
{
    // Invoked when the update handle is created
    // This happens just before setting the title, description, etc.
}

public void HandleCompletion(WorkshopItemDataCreateStatus status)
{
    // Always invoked even if a failure occurred.
    // This will tell you the results of the create and update.
    // This is only invoked after all other steps are completed.
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Note this creates an empty file ID that you can then update to add the desired content.

<figure><img src="../.gitbook/assets/image (422).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
Coming Soon
```
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### Update Item

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Use the Workshop Item Search to get the items that the player has published.&#x20;

{% hint style="info" %}
See the [List Items](workshop.md#list-items) example below..
{% endhint %}

You can use the Search My Published function to get all of the items published by the player.

<figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

In the Workshop Item component in your Workshop Item Search template, add the Edit settings. Note that this will automatically add the Events settings

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

You can attach input fields for quick edits to modify the title, description, content folder, etc., or you can pass the item a Workshop Item Editor for a more robust set of features.

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

Running the Set Editor function will load this item into the editor's memory. Note that the preview image and content folder path can't be loaded, so you will need to make sure you set those values yourself via an input field or a file/folder browser.

## C\#

This works similarly to [Create Item](workshop.md#create-item) as defined above, with 1 minor difference ... call Update instead of Create.

```csharp
// Use the Workshop Item Editor Data to build up your item
WorkshopItemEditorData data = new();
data.title = "New Item";
data.description = "My first workshop item";
data.content = new("C:\\MyModContent");
data.preview = new("C:\\MyModPreviewImage.png");

// Call update when ready
data.Update(HandleCompleted, HandleUpdateStarted);
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

Using a Published File ID such as from the Create Item process

<figure><img src="../.gitbook/assets/image (423).png" alt=""><figcaption></figcaption></figure>

You can then use the "Set Item" nodes to update each aspect of the item.

<figure><img src="../.gitbook/assets/image (424).png" alt=""><figcaption></figcaption></figure>

The following nodes are required for all items

<figure><img src="../.gitbook/assets/image (425).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
Coming Soon
```
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}

### List Items

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

Use the Workshop Item Search component to search for workshop items

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

The key and only "required" features are:

### Template

This is the object that will be spawned for each item returned by your search. This would be a Unity UI prefab that has a Workshop Item component on it, helping you "display" each of the items.

### Content

This is where each item will be parented when it's spawned. Typically, you would apply a "Layout" component to this, such as Unity's built-in Grid Layout component.

### Setting up the Workshop Item

The Workshop Item component is what you attach to your "Template" to connect data from the workshop item to your UI elements.

<figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

This is a modular component, so you can add as much or as little functionality as you need for your UI.

<figure><img src="../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

We have a prefab called "Workshop Item Search" that demonstrates this complete system, and that prefab is used in our sample scene. Consult the [installation guide](../install/unity-install.md) for more information on how to find the prefabs and samples.

When you're ready to run the search, use a Unity Button or similar and call one of the "Search" functions.

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

Options include:

* Search All\
  Returns any item found, similar to browsing in the Workshop page on Steam
* Search Favorites\
  Returns only items the player has favourited
* Search My Published\
  Returns only items the player has created
* Search Subscribed\
  Returns only items the player has subscribed to, e.g. "installed"

## C\#

<pre class="language-csharp"><code class="lang-csharp">// Create a query to find the desired items
var query = UgcQuery.Get(EUGCQuery.k_EUGCQuery_RankedByTrend
    , EUGCMatchingUGCType.k_EUGCMatchingUGCType_Items_ReadyToUse
    , AppData.Me
    , AppData.Me);
    
// Optionally filter on a search string
query.SetSearchText("Text to search");

<strong>// Run the query
</strong>query.Execute(HandleResults);

// Handle the results
void HandleResults(UgcQuery query)
{
    // Iterate over the found items
    foreach (var result in query.ResultsList)
    {
        // Do something with it
    }
}
</code></pre>
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

### Subscribed Items

You can quickly get the items the player is subscribed to e.g. are using in-game via

<figure><img src="../.gitbook/assets/image (428).png" alt=""><figcaption></figcaption></figure>

This will result in a Query Handle as with general queries but it is not "paged" meaning all items will return in a single execute.

### General Queries

<figure><img src="../.gitbook/assets/image (429).png" alt=""><figcaption></figcaption></figure>

#### Account ID

Account ID refers to the account ID of the user you want to get items for. You can obtain the account ID of a Steam User from their user ID.

<figure><img src="../.gitbook/assets/image (427).png" alt=""><figcaption></figcaption></figure>

### Configure the Query

By default a query will return minimal informaiton generally the title, short description and install path and state. You can request additional data be returned using the "Set Return" nodes.

<figure><img src="../.gitbook/assets/image (430).png" alt=""><figcaption></figcaption></figure>

### Execute Query

<figure><img src="../.gitbook/assets/image (431).png" alt=""><figcaption></figcaption></figure>

When you execute a query you are provided with the number of results returned and the total number of results matching the query.

Each page is 50 results so you can assume the total number of pages is TotalMatchingResults / 50 + 1

### Reading Results

<figure><img src="../.gitbook/assets/image (432).png" alt=""><figcaption></figcaption></figure>

The return value contains all the details about each item, note that some fields like metadata and tags may not populate unless you request them with the "Set Return" feature.

<figure><img src="../.gitbook/assets/image (433).png" alt=""><figcaption></figcaption></figure>

When complete and before creating another query, release the handle

<figure><img src="../.gitbook/assets/image (434).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
Coming Soon
```
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}



### Find Installed Content

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free&#x20;

You can find the items the player has installed by using the "Search Subscribed" option when [listing items](workshop.md#list-items). Accessing the content it downloaded however will require C# code and is up to your programmer to do.

## C\#

```csharp
// Get a query for the subscribed items
var query = UgcQuery.GetSubscribed();
// Run the query
query.Execute(HandleResults);

// Handle the results
void HandleResults(UgcQuery query)
{
    // Iterate over the found items
    foreach (var result in query.ResultsList)
    {
        // Check if its installed and download if needed
        if (!result.IsInstalled)
            result.DownloadItem(true);
        
        // Check if this item is downloading or going to download
        if (result.IsDownloading
           || result.IsDownloadPending)
            ;// handle download in progress

        // Monitor how much is downloaded
        float percentComplete = result.DownloadCompletion;

        // The location where the content is downloaded to
        result.FolderPath
    }
}
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (435).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
Coming Soon
```
{% endtab %}

{% tab title="Steamworks.NET" %}

{% endtab %}
{% endtabs %}
