---
description: Sometimes you just need a little more
---

# Json

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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
