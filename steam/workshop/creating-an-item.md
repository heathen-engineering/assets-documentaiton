# Creating an Item

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

With Heathen's Steamworks Complete creating a new workshop item from your game can be done with a [single call to our API](https://kb.heathenengineering.com/assets/steamworks/api/usergeneratedcontent.client#createitem). Understanding what data you need to send to this call is important and the cause of most issues experienced.

## [Workshop Item Data](../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item-data.md)

This is a simple `struct` we created that lets you gather up all of the inputs needed to create a new workshop item. You can find details on the [Workshop Item Data](../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item-data.md) object in its article. Here is a list of data you will need in order to create a [Workshop Item Data](../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item-data.md) object.

* **App ID**\
  This will nearly always be your game's App ID and is the ID of the app this item is made to work with. You can read this from our API easily via [App.Client.Id](../../old-toolkit-for-steamworks/unity/api-extensions/app.client.md#id).
* **Title**\
  The name you want to give to this item as a string. This must be less than 129 characters in length.
* **Description**\
  The description you want to give to this item as a string. This must be less than 8000 characters in length.
* **Content Folder**\
  This should be the full path to the content folder. Steam API will read and compress all of the contents of this folder so this folder path must be
  * A fully qualified as in the full and entire name of the folder from its root drive.
  * Accessible by the Steam Client e.g. not in a secure or hidden folder
  * Not empty ... must contain files that are to be uploaded to the item ... this should not include a zip file
  * Must not be a zip file, this must be a standard operating system folder
* **Preview Image File**\
  This should be the full path to the image file (PNG or JPG) that you would like use as the items main preview image. This file must meet these requirements
  * A fully qualified as in the full and entire name of the file path from its root drive.
  * Accessible by the Steam Client e.g. not secure or hidden
  * Less than 1mb in size
  * Less than the file size quota configured in the app's Steam Cloud Settings\
    UGC (Workshop) uses Steam Cloud to upload images and files and so you must configure sufficient room for it in [your app's cloud settings](https://partner.steamgames.com/apps/cloud/).
  * Of a valid type, JPG, PNG or GIF

In addition to the required fields you have a number of optional fields

* Metadata\
  This is string of up to 5000 characters and can be anything you like to include JSON data giving you more info about what this item is.
* Preview Files\
  A collection to image paths with the same requirements as the Preview Image File. These will be uploaded as additional images on the item and can be left null if none are wanted.
* YouTube Video Ids\
  A collection of YouTube video IDs e.g. "jHgZh4GV9G0" not the whole URL
* Tags\
  A collection of tags which must each be less than 255 characters in length. These are simple tags e.g. "Map", "Weapon", etc.
* Key Value Tags\
  Similar to tags this is a collection of "Key:Value" tags, the total length of key + value must be less than 255.

To create the item simply instantiate a new [WorkshopItemData ](../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item-data.md)object

```csharp
var itemData = new WorkshopItemData
{
    appId = API.App.Client.Id,
    title = "My New Item Title",
    description = "Item description",
    content = new System.IO.DirectoryInfo("C:/ValidFolderPath"),
    preview = new System.IO.FileInfo("C:/ValidImagePath.jpg"),
    //Now the optional ones
    metadata = "Some arbitrary string",
    tags = new[]
    {
        "tag 1",
        "tag 2"
    }
};

itemData.Create(result =>
{
    if(result.hasError)
        ; //some error
    else
        ; //seems fine
});
```

## User Generated Content API

Now that we have our data sorted we can simply call create on the UGC API.&#x20;

You probably noticed its name is very long and a pain to type? We do this so each name is verbose, easily understandable and not likely to be ambiguous. You can however make it easier for yourself in your using statements via an alias. See our [article on Namespaces](../../company/development/namespace-and-using.md) for more information.

```csharp
using UGC = HeathenEngineering.SteamworksIntegration.API.UserGeneratedContent.Client;
```

You can now access the UGC API with a much shorter name of `UGC`.

```csharp
//Usually easier to just call itemData.Create(...) but this is here if you want it
UGC.CreateItem(itemData, 
               additionalPreviews, 
               youTubeIds, 
               keyValueTags, 
               completedCallback, 
               uploadStartedCallback, 
               fileCreatedCallback);
```

Technically that is all that is required to create a workshop item ... however this would make it hard to handle any sort of issue or error so we recommend you provide a callback handler. You can learn more about [callbacks in our article here](../../company/development/callbacks.md). In the case of CreateItem it takes a callback that has a single parameter of type [WorkshopItemDataCreateStatus](../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item-data-create-status.md) and is an ideal candidate for an [anonymous callback as discussed in our article here](../../company/development/lambda-expressions.md#callbacks).

## Troubleshooting

The [EResult ](https://partner.steamgames.com/doc/api/steam_api#EResult)value returned by the callback will give you some idea as to what went wrong with any given attempt to create. Making since of this is easier if you understand the process. To create a new UGC item its actually a two step process

1. Create a new empty "file id" \
   This is just what Steam calls the entry for your Workshop item and this step rarely fails. If it does fail it suggests an issue with your app configuration or the user your logged in with.
2. Set the required values on that new empty "file id"\
   This is where we set and update the file id created in step 1 with all the data you gave us in the [Workshop Item Data](../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item-data.md) object.

Nearly 100% of the time the issue is with the data you provided to the [Workshop Item Data](../../old-toolkit-for-steamworks/unity/objects/classes/workshop-item-data.md) object. The most common issues are listed below

### Preview Image

1st make sure the path you provided is a full path to the file from the root drive its stored on.

Next make sure the path is accessible to Steam client, not protected, hidden, etc.

Next make sure the file is a valid type, JPG, PNG and GIF are recommend by Valve

Make sure the file is < 1mb in size

Make sure the file is < the quota configured in the app's [Steam Cloud Settings](https://partner.steamgames.com/apps/cloud/).

### Content Folder

1st make sure the path you provided is a full path to the folder from the root drive its stored on.

Next make sure the path is accessible to Steam client, not protected, hidden, etc.

Make sure the folder is not empty

