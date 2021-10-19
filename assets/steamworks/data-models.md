---
description: >-
  Understanding Data Models and Steam Remote Storage (aka Steam Cloud) through
  the Heathen Engineering integration
---

# Remote Storage (Cloud)

## Introduction

You can create custom data models which can be saved and loaded on Steam's "Remote Storage", aka "Steam Cloud" system with a single line of code.

![](<../../.gitbook/assets/image (14).png>)

To get started you will need to define your "data model". That is you will need to write a class or struct which is decorated with the "\[Serializable]" attribute or otherwise compatible with Unity's JsonUtility tools. We use JsonUtility to serialize your model to JSON before writing it to Steam's backend.

Once you have created your serializable class or struct, you should create a new class and inherit from DataModel providing your custom type as the T paramiter. DataModel is a ScritpableObject type and can then be created in the assets of your project and referenced to your Steam Settings object by dragging and dropping it on the drop panel.

You will notice that the DataModel base class includes a member "public string extension"

![](<../../.gitbook/assets/image (15).png>)

The extension works just like a file extension in that our system will match file names by the extension and load data from Steam into the DataModel with the matching extension. As you can see in the example you can leave this blank which means every file matches it.

## Create a DataModel

Create a new serializable structure or class to represent your data model. Note this is just an example, you can create or use any serializable class or structure you like.

```csharp
[Serializable]
public class ExampleCustomSerializable
{
    public string exampleString;
    public bool exampleBool;
    public float exampleFloat;
    public Serializable.SerializableTransform exampleTransform;
}
```

Next we create our custom class derived from DataMode{T}. This doesn't need anything in its body, the base class contains all the required logic. Don't forget to decorate the class with the CreateAssetMenu attribute so you can easily create this in your project folder.

```csharp
[CreateAssetMenu(menuName = "Steamworks/My Data Model")]
public class ExampleNewDataModel : DataModel<ExampleCustomSerializable> { }
```

Now you can create this object in your Project Tab, aka the Asset Database by simply right clicking and selecting "Create > Steamworks > My Data Model". Once done set the "Extensions" field to the desired value, remember this should be unique to this data model. It doesn't need to be human friendly, but it can be helpful to name it after something meaningful to you e.g.\
.playerProfile\
or\
.settings

## Use a DataModel

### Reference the data model

As with other examples, we will now create a reference to our Data Mode so we can access it easily in our scripts

```csharp
public ExampleNewDataModel model;
```

### Access its data

We can access the custom serializable object we based this on via the data member

```csharp
ExampleCustomSerializable dataValue = model.data;
```

### Set data values

The model object we created represents the current loaded file of this type. We can set the field in our custom serializable as you would any other field

```csharp
model.data.exampleString = "Hello World";
```

### Save to Steam

And you can save this to Steam with a simple method call

```csharp
model.Save("fileName");
```

The system will apply the extension if its missing, then will serialize the data and save that to Steam's Remote Storage.

### Load from Steam

To load a file we can do similar, note that in this case we need to add the extension to the file name as we do look for an exact string match.

```csharp
model.LoadFileAddress("fileName" + model.extension);
```

We have many overloads to the Load option including loading from a "FileAddress" object.

### List files found on Steam

FileAddress is a special object used by the availableFiles list. This list exists on each DataModel{T} and is populated by the RefreshFileList method.

So to fetch all the files available for your models

```csharp
//This refreshes the available files list on all referenced data models
RemoteStorageSystem.RefreshFileList();

foreach(var address in model.availableFiles)
{
  Debug.Log(address.fileName + " was last modified on " 
  + address.LocalTimestamp.ToString());
}
```

### Load files from listed addresses

You can use the FileAddress stored in the available files list to load data. For example if you wanted to simply load the most recent file of this type.

Note we sort the availableFiles by timestamp so its just a matter of loading the first in the list

```csharp
model.LoadFileAddress(model.availableFiles[0]);
```

## Working with raw data

You can read and write to Steam's remote storage without the need of a model if your happy to work with byte\[] data. To do so you will be using the `RemoteStroageSystem` directly, this is what a DataModel is doing for you on the back end so you will get the same results as DataModel with a bit less convenance.

{% hint style="info" %}
Asynchronious versions of all methods exist and differ only in that they return a RemoteStorageDataFile which can be used to track status and take a callback which can be used to notify on completion.
{% endhint %}

### File Read

You can read file data out in a number of ways but for working with data raw your most likely going to use&#x20;

#### For byte\[] Data

```csharp
byte[] fileData = RemoteStroageSystem.FileReadData(string fileName);
```

or

```csharp
byte[] fileData = RemoteStroageSystem.FileReadData(FileAddress address);
```

#### For String Data

```csharp
string fileData = RemoteStroageSystem.FileReadString(string fileName, 
                                                     Encoding encoding);
```

or

```csharp
string fileData = RemoteStroageSystem.FileReadString(FileAddress address, 
                                                     Encoding encoding);
```

#### For JSON Data

Where ObjectType is the serializable object to cast the result to

```csharp
ObjectType fileData = RemoteStroageSystem.FileReadJson<ObjectType>(string fileName, 
                                                                   Encoding encoding);
```

or

```csharp
ObjectType fileData = RemoteStroageSystem.FileReadJson<ObjectType>(FileAddress address, 
                                                                   Encoding encoding);
```

### File Write

Writing files in the raw form works much the same

#### For byte\[] Data

```csharp
RemoteStroageSystem.FileWrite(string fileName, byte[] data);
```

#### For String Data

```csharp
RemoteStroageSystem.FileWrite(string fileName, string data, Encoding encoding);
```

#### For JSON Data

```csharp
RemoteStroageSystem.FileWrite(string fileName, object data, Encoding ecoding);
```
