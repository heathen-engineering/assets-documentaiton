# Remote Storage

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

```csharp
public static class API.RemoteStorage
```

The whole of the remote storage system is only accessable from the Client API as a result you will always be using the form:

```csharp
API.RemoteStorage.Client
```

### What can it do?

Remote storage is primarly used to save game data and other user specific information to a cloud storage area. This insures that data is available wherever the player chooses to play.

The API makes it easy to read and write files to and from Steam Remote Storage aka Steam Cloud save.

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/data-model" %}

## Events

### Local File Change

If a Steam app is flagged for supporting dynamic Steam Cloud sync, and a sync occurs, this callback will be posted to the app if any local files changed.

## How To

### Delete a File

Deletes a file from the local disk, and propagates that delete to the cloud.

```csharp
var result = API.RemoteStorage.Client.FileDelete(file);
```

A common alternative is to simply forget the file, that is leave the file on the local disk but remove it from the cloud.

```csharp
var result = API.RemoteStorage.Client.FileForget(file);
```

Deletes the file from remote storage, but leaves it on the local disk and remains accessible from the API.

### Check for File

Checks whether the specified file exists.

```csharp
var result = API.RemoteStorage.Client.FileExists(file);
```

### Reading a File

Heathen has provided a number of easy to use read operations so you can get at your file data as fast as possible.&#x20;

```csharp
byte[] data = API.RemoteStorage.Client.FileRead(file);
```

```csharp
string text = API.RemoteStorage.Client.FieldReadString(file, encoding);
```

```csharp
[Serializable]
public MySerializableData
{
    public int someData;
    // ... anything that is searialziable can go here
}

// To read it
var result = API.RemoteStorage.Client.FileReadJson<MySerializableData>(file, encoding);
```

```csharp
API.RemoteStorage.Client.FileReadAsync(file, callback);
```

### Sharing Files

File sharing is a feature used by Leaderboards to attach complex bits of data such as videos or replays.

```csharp
API.RemoteStorage.Client.FileShare(file, callback);
```

You can then use

```csharp
var data = API.RemoteStorage.Client.UGCRead(handle);
```

To read a shared file, the [Leaderboard ](leaderboards.md)interface though will do this for you

### Writing Files

Writing files is made just as simple as reading, with multiple options depending on your needs. Asynchronious options are available for all variations.

```csharp
byte[] fileData;
//...
API.RemoteStorage.Client.FileWrite(file, fileData);
```

```csharp
string fileData;
//...
API.RemoteStorage.Client.FileWrite(file, fileData, encoding);
```

```csharp
SomeSerializableObject fileData;
//...
API.RemoteStorage.Client.FileWrite(file, fileData, encoding);
```

### File Streaming

Open, write, close and cancel file streams.

```csharp
var handle = API.RemoteStorage.Client.FileWriteStreamOpen(file);
```

```csharp
API.RemoteStorage.Client.FileWriteStreamWriteChunk(handle, data);
```

```csharp
API.RemoteStorage.Client.FileWriteStreamClose(handle);
```

```csharp
API.RemoteStorage.Client.FileWriteStreamCancel(handle);
```

### Managing Files

You can get a collection of all the files stored for this app for this user which will return as an array of [RemoteStorageFile](../objects/remote-storage-file.md) objects

```csharp
var result = API.RemoteStorage.Client.GetFiles();
```

optionally you can get just the files that have a given extension, this can be useful for selecting just profiles, or settings or characters and so on.

```csharp
var characters = API.RemoteStorage.Client.GetFiles(".char");
```

### Check Storage Limits

Its important to check if the user has enabled and has the room to store the files you want to save.

```csharp
if(API.RemoteStorage.Client.IsEnabledForAccount)
    Debug.Log("The account has it turned on");

if(API.RemoteStorage.Client.IsEnabledForApp)
    Debug.Log("The user has it enabled for the app so does the dev");

if(API.RemoteStorage.Client.IsEnabled)
    Debug.Log("Both of the above are ture");
```

```csharp
if(API.RemoteStorage.Client(out ulong total, out ulong remaining))
{
    var used = (double)remaining/(double)total;
    Debug.Log(used.ToString("P2)") + " or ["+ remaining +"] bytes remaining ");
    // 50% or [1024] bytes remaining
}
```
