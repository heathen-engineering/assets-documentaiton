# Data Model

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public class DataModel<T>: DataModel
```

```csharp
public class DataModel : ScriptableObject
```

{% hint style="info" %}
Learn more about this topic in the [DataModel Programming Tools](../unity-engine/programming-tools/datamodel.md) guide.
{% endhint %}

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
You do not need to write any code in the body of the DataModel, the base class will implement everything you need for you.
{% endhint %}

Once complete you can use your new ScriptableObject to represent the currently loaded copy of this data type and you can use its member functions to list the available files of this type as seen on [Steam Remote Storage](../api/remote-storage.md) and to read and write given files.
