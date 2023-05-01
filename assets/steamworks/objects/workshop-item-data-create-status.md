# Workshop Item Data Create Status

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Used with the [User Generated Content interface](../api/user-generated-content.md#createitem) and the [WorkshopItemData ](../data-layer/workshop-item-data.md)tool.

The structure provides details on the completed create operation including access to the resulting Workshop Item and the native callback results from Steam API.

```csharp
public struct WorkshopItemDataCreateStatus
{
    public bool hasError;
    public string errorMessage;
    public WorkshopItemData data;
    public CreateItemResult_t? createItemResult;
    public SubmitItemUpdateResult_t? submitItemUpdateResult;
}
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

### data

The [WorkshopItemData ](../data-layer/workshop-item-data.md)that created this response and that contains details about the object.

```csharp
public WorkshopItemData data;
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
