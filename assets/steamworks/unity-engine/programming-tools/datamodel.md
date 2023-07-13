# DataModel

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

An abstract class that can be inherited from in order to create custom serializable data types for use with Steam Remote Storage. The idea is that you create a serializable data type defining the fields you wish to include in the file and can then create an object to represent that file type which has easy access to Steam Remote Storage.

```csharp
using HeathenEngieering.SteamworksIntegration.UI;
```

```csharp
public abstract class DataModel<T> : DataModel
```

## Example

```csharp
[Serializable]
public struct MyCustomData
{
    public string name;
    public float health;
    public int level;
    public int currency;
}
```

```csharp
public class MyCustomDataModel : DataMode<MyCustomData>
{ }
```

with this done you can now easily create and save or load data as `MyCustomData` for example

```csharp
//Create the data
//myModel.data is now the current in memory state for the current instance
var myModel = new MyCustomDataModel();
myModel.extension = ".data";
myModel.data = new MyCustomData
{
  name = "Helo world",  
  health = 46.5f,
  level = 13,
  currency = 1123
};

//Save the data
myModel.Save("New Data Save File");

//Get all .data files stored on Steam for this user
myModel.Refresh();
foreach(var file in myModel.availableFiles)
  Debug.Log($"{file.name}, {file.timestamp}");

//Load the first file found
myModel.LoadFileAddress(myModel.availableFiles[0]);
```

## Events

### Data Updated

```csharp
public UnityEvent evtDataUpdated;
```

This event is raised when a new file has been loaded into memory for this model.

## Fields and Attributes

### extension

```csharp
public string extension;
```

What if any extension should be added to the file, defining this allows the system to assume what files belong to what data model e.g. all files whose extensions match this value are assumed to be compatible with this model.

This means you can create a .dat model and a .profile model and trust that the system can identify and load the proper files to the proper models.

### Available Files

```csharp
public RemoteStorageFile[] availableFiles;
```

The collection of all Steam Remote Storage files found to match this model.

### Data Type

```csharp
public abstract Type DataType => get;
```

Gets the base type of the data stored by this model

### Data

```csharp
public T data;
```

Stores the current instance of the data in local memory

## Methods

### Refresh

```csharp
public void Refresh()
```

checks Steam for files that match this model and populates the Available Files collection.

### Load Byte Array

```csharp
public void LoadByteArray(byte[] data)
```

loads data from a byte array

### Load Json

```csharp
public void LoadJson(string json)
```

loads data from a json formatted string

### Load File Address

```csharp
public void LoadFileAddress(RemoteStorageFile address)
```

```csharp
public void LoadFileAddress(string address)
```

Loads data from a file on Steam Remote Storage&#x20;

### Load File Address Async

```csharp
public void LoadFileAddressAsync(RemoteStorageFile address, 
                                          Action<bool> callback)
```

```csharp
public void LoadFileAddressAsync(string address, 
                                          Action<bool> callback)
```

Loads data from a file on Steam Remote Storage, the callback will be invoked when the load has completed.

### To Byte Array

```csharp
public byte[] ToByteArray()
```

Converts the current in memory data to a byte\[]

### To Json

```csharp
public string ToJson()
```

Converts the current in memory data to a json formatted string

### Save

```csharp
public bool Save(string filename)
```

Saves the data to Steam Remote Storage with a given name, this will append the extension if defined.

### Save Async

```csharp
public bool SaveAsync(string filename, 
                      Action<RemotStorageFileWriteAsyncComplete_t, bool> callback)
```

Saves the data to Steam Remote Storage with a given name, this will append the extension if defined. The callback will be invoked when the operation is completed.
