# Cloud Save

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% embed url="https://partner.steamgames.com/doc/features/cloud" %}

Quote from Valve's documentation

> The Steam Cloud provides an easy and transparent remote file storage system for your game. Files specified in the Auto-Cloud configuration or written to disk (created, modified, deleted, etc.) using the Cloud API will automatically be replicated to the Steam servers after the game exits.
>
> If the user changes computers, the files are automatically downloaded to the new computer prior to the game launching. The game can then access the files by reading them through the Cloud API or reading them directly from disk as usual. Avoid machine specific configurations such as video settings.
>
> The Steam Client does the work of ensuring that the files are kept synchronized across all computers the user may be accessing.
>
> Users can globally disable Cloud synchronization in the Steam Settings under Cloud by unchecking "Enable Steam Cloud synchronization for applications which support it."

## Remote Storage API

You can use the Remote Storage API to access Steam's remote storage features.

```csharp
using CloudAPI = HeathenEngineering.SteamworksIntegration.API.RemoteStorage.Client;
```

It is important that you check and insure that the user has enabled cloud storage and that the user has sufficent storage space remaining when writing new files to the system

### Is the system enabled?

```csharp
if(CloudAPI.IsEnabled)
{
    //Yes it is
}
else
{
    //No it is not
}
```

If the IsEnabled field is false it could be for one of two reasons.

```csharp
//Does the user have it turned on
if(CloudAPI.IsEnabledForAccount)
{
    //The user has enabled cloud storage
}
else
{
    //The user has disabled cloud storage for this app
}

//Does the developer (and Valve) have it turned on
if(CloudAPI.IsEnabledForApp)
{
    //You have enabled cloud storage in the app configuration
}
else
{
   //You or Valve have disabled cloud storage in the app configuraiton
}
```

### Storage Space

To check the user's storage space

```csharp
CloudAPI.GetQuota(out ulong total, out ulong remaining);

Debug.Log("Used " + total-remaining + " of " + total + " bytes.");
```

### List Files

```csharp
RemoteStorageFile[] files = CloudAPI.GetFiles();
```

GetFiles returns a list of all files found on Steam and returns an array of [RemoteStorageFile](../../objects/remote-storage-file.md) objects. The RemoteStorageFile object can be thought of similar to the .NET FileInfo object and contains data about the file that can be used to perform other actions.

You can optionally return files that have a specific extension such as ".profile"

```csharp
RemoteStorageFile[] files = CloudAPI.GetFiles(".profile");
```

### Read Files

The RemoteStorageFile object returned can be used to read the data of files as a byte\[], string or to cast the data to any serializable data type.

Assuming a serializable data type `MyDataType`

Assuming a file RemoteStorageFile named dataFile:

```csharp
//Get byte[]
byte[] data = dataFile.Data;

//Get string
string text = dataFile.ToString();

//Get object
MyDataType obj = dataFile.ToJson<MyDataType>();
```

Alternativly you if you know the name of the file you can read it directly from the API

```csharp
//Get byte[]
byte[] data = CouldAPI.FileRead("TheFilesName");

//Get string
string text = CloudAPI.FileReadString("TheFilesName", System.Text.Encoding.UTF8);

//Get object
MyDataType obj = CloudAPI.FileReadJson<MyDataType>("TheFilesName", System.Text.Encoding.UTF8);
```

If you prefer you can read the files asynchroniously&#x20;

```csharp
//Get byte[]
CouldAPI.FileReadAsync("TheFilesName", (data, hasError) =>
   {
      if(!hasError)
      {
         //data is your byte[]
      }
   });
```

### Write File

You can write a file to the remote storage system using the following methods

```csharp
//Save a byte[]
CloudAPI.FileWrite("TheFileName", data);

//Save a string
CloudAPI.FileWrite("TheFileName", data, System.Text.Encoding.UTF8);

//Save an object
CloudAPI.FileWrite("TheFileName", data, System.Text.Encoding.UTF8);
```

The same commands can be used asynchroniously

```csharp
CloudAPI.FileWriteAsync("TheFileName", data, (result, hasError) =>
    {
        if(!hasError)
            Debug.Log("File written");
    });
```

## Data Model

The Data Model concept is a tool that helps you manage each type of save file your game works with. To get started you would first need to create the "structure" of your file as a serializable object. This can be a class or structure ... in general you should always use a structure unless your object specifically needs features of C# class not available to C# structures.

### Creating a model

```csharp
[System.Serializable]
public struct SaveProfile
{
    public int difficulty;
    public string characterName;
    public int characterLevel;
    public int characterClass;
    //etc.
}
```

Once you have defined your data structure you can create a new DataModel object which will help you list, load, save and generally manage all examples of this file on the users Steam storage.

```csharp
[CreateAssetMenu(menuName = "My Data/Save Profile")]
public class SaveProfileDataModel : DataModel<SaveProfile>
{ }
```

Note that we do not need to write any code in the body of the SaveProfileDataModel class, everything is implemented for you by the DataModel\<T> base class.

Once this is done you can create a Scriptable Object in your project's asset folder by right clicking and selecting `Create > My Data > Save Profile` . You can use this new object to assign an extension. This extension will be added to the end of the file name if missing and is how the DataModel knows which files belong to it.

### Referencing your model

With your new DataModel you can more easily list, load and save character profiles; lets assume we have a reference to our DataModel such as:

```csharp
public SaveProfileDataModel profiles;
```

### Listing files that match your model

We can now refresh the list of profiles the user has saved with a simple call that can even be connected to Unity Events such as a button click.

```csharp
profiles.Refresh();
```

This will update the list of available files which we can iterate over via

```csharp
foreach(var file in profiles.availableFiles)
{
    Debug.Log("Found a file named: " + file.name);
}
```

### Loading data for your model

You can load a file by calling

```csharp
profiles.LoadFileAddress(file);
```

This will load the file information to the data field which can be accessed via

```csharp
Debug.Log("Difficulty Setting = " + profile.data.difficulty);
Debug.Log("Character Name = " + profile.data.characterName);
//etc.
```

### Saving data

You can modify and save the data managed by your model:

```csharp
profiles.data.difficulty = 3;
profiles.Save("profileSettings");
```

Note the save method will add the extension if its missing and has overloads for aynchronious save.
