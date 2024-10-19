# Subscribed Items

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Workshop lets your users create and upload items and then subscribe to other user's items to extend and enhance there game. This article will go over the tools available for detecting what items the user is "subscribed" to and how to find more information about those items such as where they are installed so you can load their content.

## Finding the subscribed items

The simplest approach to find what items the user is subscribed to is to use the [UGCQuery](../../toolkit-for-steamworks/unity/classes-and-structs/ugc-query.md) tool and search for all subscribed items.&#x20;

```csharp
var query = UgcQuery.GetSubscriobed();
```

This will give you a [UgcQuery ](../../toolkit-for-steamworks/unity/classes-and-structs/ugc-query.md)object configured to return the list of items the local user is subscribed to. You can further adapt this query to suit your own needs. For example if your game's items use metadata then you should set the query to also return metadata.

```csharp
query.SetReturnMetadata(true);
```

Once your query is configured as required you can simply execute the query and iterate over its results.

```csharp
query.Execute(callback);
```

results will be a reference to the same [UgcQuery ](../../toolkit-for-steamworks/unity/classes-and-structs/ugc-query.md)this allows you to use a pre-defined method such as

```csharp
query.Execute(HandleQueryResults);
```

where

```csharp
void HandleQueryResults(UgcQuery results)
{
    //Do Work
}
```

Or you can use expression to create an anonymous method to handle the results such as

```csharp
query.Execute(results =>
{
    //Do Work
});
```

These are functionally the same.

## Using the results

Once you have executed your query and have a list of results you need to use those results to do what your game needs. Typically this would be to load the content stored on the item and possibly to read its metadata.

```csharp
void HandleQueryResults(UgcQuery results)
{
    foreach(item in results.ResultsList)
    {
        //The FolderPath is the DirectoryInfo of the folder 
        //the item content is located in
        Debug.Log("Content present in " + item.FolderPath.FullName);
        
        //The metadata string is the metadata found if any 
        Debug.Log("Content metadata: " + item.metadata);
    }
}
```
