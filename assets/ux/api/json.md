---
description: Sometimes you just need a little more
---

# Json

## Introduction

The Json interface is a simple helper tool that cleans up an issue with Unity's JsonUtility where in an array of Json objects cannot be read directly.

```json
[
    {
        "field" : "value"
    },
    {
        "field" : "value"
    }
}
```

The above JSON is offten returned from Web interfaces and similar that wish to return an array of JSON objects. However Unity's JSON Utility cannot handle this case as it expects an object to wrap such a list. To correct this we have create a tool that will repair such JSON strings and proivded a means to serialize any such object.

```csharp
var cleanString = API.Json.ArrayWrapper(dirtyJson);
```

The result of this would be

```json
{
    [
        {
            "field" : "value"
        },
        {
            "field" : "value"
        }
    ]
}
```

This is a valid JSON string that Unity's JsonUtility can handle. When you know you have a JSON string that starts with an array of objects as shown in the first code snipit you can clean and deserialize the result to a list in a 1 line call

```csharp
var resultList = API.Json.FetchArray<dataType>(jsonString);
```

This will return a List of the data type provided.
