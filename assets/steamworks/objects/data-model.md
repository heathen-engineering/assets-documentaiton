# Data Model

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public class DataModel<T>: DataModel
```

```csharp
public class DataModel : ScriptableObject
```

It is intended that you use this to create your core save files as Scriptable Objects. This makes it trivial to query the [Steam Remote Storage](../api/remote-storage.md) interface for records of this file type and to load data into a usable point in memory that can easily be referenced by Unity components.

You would typically start by defining your underlying data type e.g. a serializable object that represents the data you wish to save

```csharp
[Serializable]
public class MyCharacterData
{
    public string characterName;
    public int level;
    public float3 position;
    public quaternion rotation;
    //... etc.
}
```

You would then create your DataModel

```csharp
[CreateAssetMenu(menuName = "My Objects/Character Data Model")]
public class CharacterDataModel : DataModel<MyCharacterData>
{ }
```

{% hint style="success" %}
You do not need to write any code in the body of the DataModel, the base class will implament everything you need for you.
{% endhint %}

Once complete you can use your new ScriptableObject to represent the currently loaded copy of this data type and you can use its member funcitons to list the available files of this type as seen on [Steam Remote Storage](../api/remote-storage.md) and to read and write given files.

## Fields and Attributes

| Type                 | Name           | Comment                                               |
| -------------------- | -------------- | ----------------------------------------------------- |
| string               | extension      | The extension to be used with this model              |
| RemoteStorageFile\[] | availableFiles | List of available files found on Steam Remote Storage |
| Type                 | DataType       | The underlying data type used by this model           |
| T                    | data           | The data stored by this model                         |

## Methods

### Refresh

```csharp
public void Refresh();
```

Reads the list of available files from the [remote storage](../api/remote-storage.md) interface and stores them in the availabelFiles collection

### Load Data

```csharp
public void LoadByteArray(data);
```

```csharp
public void LoadJson(data);
```

```csharp
public void LoadFileAddress(address);
```

Manually loads data into the model's data field

### Export Data

```csharp
public byte[] ToByteArray();
```

Outputs the current data as a byte\[]

```csharp
public string ToJson();
```

Outputs the current data as a JSON string

### Save Data

```csharp
public void Save(fileName);
```

Saves the current data to the Steam Remote Storage system with the indicated file name
