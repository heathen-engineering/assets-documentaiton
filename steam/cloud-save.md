# ☁️ Cloud Save

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Cloud save also known as Steam Remote Storage allows you to save a file and have it synced to the "cloud" e.g. Steam's servers so that the same file is available to that user on any machine they log into.

Quote from Valve's documentation

> The Steam Cloud provides an easy and transparent remote file storage system for your game. Files specified in the Auto-Cloud configuration or written to disk (created, modified, deleted, etc.) using the Cloud API will automatically be replicated to the Steam servers after the game exits.
>
> If the user changes computers, the files are automatically downloaded to the new computer before the game launches. The game can then access the files by reading them through the Cloud API or reading them directly from the disk as usual. Avoid machine-specific configurations such as video settings.
>
> The Steam Client does the work of ensuring that the files are kept synchronized across all computers the user may be accessing.
>
> Users can globally disable Cloud synchronization in the Steam Settings under Cloud by unchecking "Enable Steam Cloud synchronization for applications which support it."

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/features/cloud](https://partner.steamgames.com/doc/features/cloud)

</details>

### Steam Remote Storage

{% hint style="success" %}
The Best Way
{% endhint %}

aka the Steam Cloud API. This is the superior method in every way and when you're using Heathen's Steamworks Complete it's easier to code for than writing a text file to disk so it's also the easier method.

### Steam Auto-Cloud

{% hint style="danger" %}
Not Recommended
{% endhint %}

Steam Auto-Cloud is an alternative to the Steam Cloud API that allows apps to use Steam Cloud without writing code or modifying the game in any way. It only requires that you specify the file groups which you want persisting in the Cloud. Steam will automatically sync the groups of files when the application launches and exits.&#x20;

While this might appear simpler on the surface it doesn't save you any effort at all in that you must still write code to read and write your files to the user's local disk. That code is no simpler and is in most cases more complex than the code required to save directly to Steam Cloud API using Heathen's Steamworks Complete.

In addition, this gives you no control over what is saved, it will attempt to sync everything in that folder so of course you do not want to store system-specific things there as that would interfere with running the game on other systems and you do not want to store large things that shouldn't be synced there. This means you end up needing to manage multiple save locations.

For more information on Steam's Auto Cloud and its configuration [read this article](https://partner.steamgames.com/doc/features/cloud#steam\_auto-cloud).

## Unity Examples

You can use the Remote Storage API to access Steam's remote storage features.

```csharp
using CloudAPI = HeathenEngineering.SteamworksIntegration.API.RemoteStorage.Client;
```

you must check and ensure that the user has enabled cloud storage and that the user has sufficient storage space remaining when writing new files to the system

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
   //You or Valve have disabled cloud storage in the app configuration
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

GetFiles returns a list of all files found on Steam and returns an array of [RemoteStorageFile](../toolkit-for-steamworks-sdk/unity/classes-and-structs/remote-storage-file.md) objects. The RemoteStorageFile object can be thought of as similar to the .NET FileInfo object and contains data about the file that can be used to perform other actions.

You can optionally return files that have a specific extension such as ".profile"

```csharp
RemoteStorageFile[] files = CloudAPI.GetFiles(".profile");
```

### Read Files

The RemoteStorageFile object returned can be used to read the data of files as a byte\[], or string or to cast the data to any serializable data type.

Assuming a serializable data type `MyDataType`

Assuming a file RemoteStorageFile named dataFile:

```csharp
//Get byte[]
byte[] data = dataFile.Data;

//Get string
string text = dataFile.ToString();

//Get an object
MyDataType obj = dataFile.ToJson<MyDataType>();
```

Alternatively, if you know the name of the file you can read it directly from the API

```csharp
//Get byte[]
byte[] data = CouldAPI.FileRead("TheFilesName");

//Get string
string text = CloudAPI.FileReadString("TheFilesName", System.Text.Encoding.UTF8);

//Get an object
MyDataType obj = CloudAPI.FileReadJson<MyDataType>("TheFilesName", System.Text.Encoding.UTF8);
```

If you prefer you can read the files asynchronously&#x20;

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
//Save a byte[] ... assumes data is a byte[]
CloudAPI.FileWrite("TheFileName", data);

//Save a string ... assumes data is a string
CloudAPI.FileWrite("TheFileName", data, System.Text.Encoding.UTF8);

//Save an object ... assumes data is a serializable class or struct
CloudAPI.FileWrite("TheFileName", data, System.Text.Encoding.UTF8);
```

The same commands can be used asynchronously

```csharp
CloudAPI.FileWriteAsync("TheFileName", data, (result, hasError) =>
    {
        if(!hasError)
            Debug.Log("File written");
    });
```

### Data Model

The Data Model concept is a tool that helps you manage each type of save file your game works with. To get started you would first need to create the "structure" of your file as a serializable object. This can be a class or structure ... in general, you should always use a structure unless your object specifically needs features of a C# class not available to C# structures.

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

Once you have defined your data structure you can create a new DataModel object which will help you list, load, save and generally manage all examples of this file on the user's Steam storage.

```csharp
[CreateAssetMenu(menuName = "My Data/Save Profile")]
public class SaveProfileDataModel : DataModel<SaveProfile>
{ }
```

Note that we do not need to write any code in the body of the SaveProfileDataModel class, everything is implemented for you by the DataModel\<T> base class.

Once this is done you can create a Scriptable Object in your project's asset folder by right-clicking and selecting `Create > My Data > Save Profile` . You can use this new object to assign an extension. This extension will be added to the end of the file name if missing and is how the DataModel knows which files belong to it.

### Referencing your model

With your new DataModel you can more easily list, load and save character profiles; let's assume we have a reference to our DataModel such as:

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

Note the save method will add the extension if it's missing and has overloads for the asynchronous save.

## Unreal Examples

We have created a Steam Remote Storage Save Game class that extends Unreal's Save Game concept enabling it to work with Steam Remote Storage. You can use this as you would any typical Save Game in Unreal.

{% hint style="info" %}
Steam Remote Storage Save Game is derived from Unreal's Save Game class. As a result, it does everything a normal Save Game object would and can be used for traditional to-disk save operation if you so desire.\
\
We have simply provided additional functions that can be used to read and write the data to and from Steam's Remote Storage system.
{% endhint %}

{% hint style="info" %}
Steam Remote Storage aka Steam Cloud Save\
Is a drop box-like file sync system that synchronizes files written to the local disk to Steam's remote storage (aka cloud). It does work in offline mode and handles syncing data between all devices the user plays on.
{% endhint %}

### Save Game Setup

Start by creating a blueprint class and here we will choose the Steam Remote Storage Save Game as our base class.

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Next, add whatever variables you would like to have saved.

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

And that is all that is required to create your Save Game object. Creating, setting and reading values from the Save Game object is the same as you would use with any Unreal Save Game object.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption><p>Assume Test Save Game is my Blueprint derived from Steam Remote Storage Save Game</p></figcaption></figure>

### Write File (aka Save)

To save the file to Steam Remote Storage you will use the Steam Write File and Steam Write File Async Blueprint functions

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Synchronious File Write</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Asynchronious File Write</p></figcaption></figure>

### Read File (aka Load)

To read the file from Steam Remote Storage you will use the Steam Read File and Steam Read File Sync Blueprint functions

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Synchronious File Read</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Asynchronious File Read</p></figcaption></figure>
