# Workshop Item Data Create Status

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Used with the User Generated Content interface for [1 line creation](../api/user-generated-content.md#create-and-update-items) of workshop items as the paramiter in the callback e.g.

```csharp
public static bool CreateItem(
        WorkshopItemData item, 
        Action<WorkshopItemDataCreateStatus> callback = null)
```

This method is part of the [User Generated Content API](../api/user-generated-content.md), you provide it with two paramiters.

### WorkshopItemData

The first paramiter, this defines the data of the item you want to create.

### Action\<WorkshopItemDataCreateStatus>

The second paramiter, this is a deligate to a method that will be called when the process is complete. That deligate expects a method that takes 1 paramiter of type WorkshopItemDataCreateStats (this object)&#x20;

### Example Call

```csharp
var itemData = new WorkshopItemData
    {
        // Set the paramiters of this object
    };

API.UserGeneratedContent.Client.CreateItem(itemData, (status) =>
    {
        if(status.hasError)
        {
            //Something went wrong
            Debug.LogError(status.errorMessage);
        }
    });
```

## Definition

```csharp
public struct WorkshopItemDataCreateStatus
```

### Fields and Attributes

### hasError

Indicates rather or not this process ended in error. This will be true if either the create or update steps had a fault.

```csharp
public bool hasError;
```

### errorMessage

If any this will contain the error message related to the fault.

```csharp
public string errorMessage;
```

### ugcFileId

This is the ID of the UGC file that was created as is used by the [User Generated Content API](../api/user-generated-content.md). This is a nullable value.

```csharp
public PublishedFileId_t? ugcFileId;
```

### createItemResult

This is the result status returned by Valve when the create step completes, If this is not a successful result then there will not be a submit item update result. This is a nullable value.

```csharp
public CreateItemResult_t? createItemResult;
```

### submitItemUpdateResult

This is the result of the update item status returned by Valve when the update step completes. This is a nullable value.

```csharp
public SubmitItemUpdateResult_t? submitItemUpdateResult;
```
