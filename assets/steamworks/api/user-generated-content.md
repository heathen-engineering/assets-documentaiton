# User Generated Content

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

```csharp
public static class API.UserGeneratedContent
```

Client features are available under the client interface

```csharp
API.UserGeneratedContent.Client
```

### What can it do?

Create, download, browse and edit Steam UGC files aka Steam Workshop.

### Related Components

{% embed url="https://kb.heathenengineering.com/assets/steamworks/components/ugc-query-manager" %}

### Related Obejcts





## Events

### Item Downloaded

Occures when a UGC item is downloaded

### Workshop Item Installed

Called when a workshop item has been installed or updated

## How To

### Create and Update Items

Creating a new item can be done in one of two ways.

One liner

```csharp
API.UserGeneratedContent.Client.CreateItem(itemdata, callback);
```

Step by step

```csharp
API.UserGeneratedContent.Client.CreateItem(appId, callback);
```

This callback will contain a UGCUpdateHandle\_t which can be used by other methods to update key features using the following methods

You can also use these tools to modify and existing file assuming you are its author

```csharp
API.UserGeneratedContent.Client.StartItemUpdate(appId, fileId);
```

* SetItemContent
* SetItemDescription
* SetItemMetadata
* SetItemPreview
* SetItemTags
* SetItemTitle
* SetItemUpdateLanguage
* SetItemVisibility
* UpdateItemPreviewVideo
* UpdateItemPreviewFIle
* UpdateItemPreviewVideo

When complete you should submit the update

```csharp
API.UserGeneratedContent.Client.SubmitItemUpdate(handle, changenote, callback);
```

### Browse Items

The easiest way to handle a UGC / Workshop browser in game is to use the [UGC Query Manager](../components/ugc-query-manager.md). The manager uses the same features present in the interface so it can be done manually.

### Get Subscribed Items

To get the list of subscirbed items e.g. items the user has indicated should be installed

```csharp
var results = API.UserGeneratedContent.Client.GetSubscribedItems();
```

