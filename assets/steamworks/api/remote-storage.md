# RemoteStorage.Client

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
using RemoteStorage = HeathenEngineering.SteamworksIntegration.API.RemoteStorage.Client;
```

```csharp
public static class RemoteStorage.Client
```

### What can it do?

Remote storage is primarily used to save game data and other user specific information to a cloud storage area. This insures that data is available wherever the player chooses to play.

The API makes it easy to read and write files to and from Steam Remote Storage aka Steam Cloud save.

### Related Objects

{% embed url="https://kb.heathenengineering.com/assets/steamworks/objects/data-model" %}

### Understanding Callbacks

A callback is a delegate similar to a UnityEvent, that is its a pointer to a method that will be called at some later point ... in the case of Steam methods it gets called when the process completes.

To learn more please read the article on [Callbacks](broken-reference) and on [Lambda Expressions](broken-reference).

## Events

### EventLocalFileChange

If a Steam app is flagged for supporting dynamic Steam Cloud sync, and a sync occurs, this callback will be posted to the app if any local files changed.

You would add a listener on this event such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(RemoteStorageLocalFileChange_t arg0)
{
}
```

Then you would register the event such as:

```csharp
API.Inventory.Client.EventLocalFileChange.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behavior using it is destroyed

```csharp
void OnDestroy()
{
    API.Inventory.Client.EventLocalFileChange.RemoveListener(HandleEvent);
}
```

## Fields and Attributes

### IsEnabledForAccount

```csharp
public static bool IsEnabledForAccount => get;
```

This checks if the SteamRemoteStorage API is enabled for this account.

### IsEnabledForApp

```csharp
public static bool IsEnabledForApp;
```

This checks if the SteamRemoteStroage API is enabled for this app (as in did you enabled it in the developer portal).

You can set this value to enable the remote storage API for this app.

```csharp
API.RemoteStorage.Client.IsEnabledForApp = true;
```

### IsEnabled

This returns true if both IsEnabledForAccount and IsEnabled are true.

```csharp
public static bool IsEnabled => get;
```

## Methods

### FileDelete

```csharp
public static bool FileDelete(string file)
```

Deletes a file from the local disk, and propagates that delete to the cloud.

This is meant to be used when a user actively deletes a file. Use FileForget if you want to remove a file from the Steam Cloud but retain it on the users local disk.

### FileExists

```csharp
public static bool FileExists(string file)
```

Checks whether the specified file exists.

### FileForget

```csharp
public static bool FileForget(string file)
```

Deletes the file from remote storage, but leaves it on the local disk and remains accessible from the API.

When you are out of Cloud space, this can be used to allow calls to FileWrite to keep working without needing to make the user delete files.

How you decide which files to forget are up to you. It could be a simple Least Recently Used (LRU) queue or something more complicated.

Requiring the user to manage their Cloud-ized files for a game, while is possible to do, it is never recommended. For instance, "Which file would you like to delete so that you may store this new one?" removes a significant advantage of using the Cloud in the first place: its transparency.

Once a file has been deleted or forgotten, calling FileWrite will resynchronize it in the Cloud. Rewriting a forgotten file is the only way to make it persisted again.

### FileRead

```csharp
public static byte[] FileRead(string file)
```

Opens a binary file, reads the contents of the file into a byte array, and then closes the file.

### FileReadString

```csharp
public static string FileReadString(string fileName, System.Text.Encoding encoding)
```

Reads the data from the file as text

### FileReadJson

```csharp
public static T FileReadJson<T>(string fileName, System.Text.Encoding encoding)
```

Reads the data from the file as a JSON object

### FileReadAsync

```csharp
public static void FileReadAsync(string file, Action<byte[], bool> callback)
```

Starts an asynchronous read from a file.

### FileShare

```csharp
public static void FileShare(string file, Action<RemoteStorageFileShareResult_t, bool> callback)
```

Marks a file to be shared, this is used by the leaderboard attachment system and a few other use cases.

### FileWrite

May return false under the following conditions: \
The file you're trying to write is larger than 100MiB as defined by k\_unMaxCloudFileChunkSize. \
cubData is less than 0. \
pvData is NULL. \
You tried to write to an invalid path or filename.Because Steamworks Cloud is cross platform the files need to have valid names on all supported OSes and file systems. See Microsoft's documentation on Naming Files, Paths, and Namespaces. \
The current user's Steamworks Cloud storage quota has been exceeded. They may have run out of space, or have too many files. \
Steamworks could not write to the disk, the location might be read-only.

```csharp
public static bool FileWrite(string file, byte[] data)
```

Creates a new file, writes the bytes to the file, and then closes the file. If the target file already exists, it is overwritten.

```csharp
public static bool FileWrite(string file, string body, System.Text.Encoding encoding)
```

Creates a new file, writes the bytes to the file, and then closes the file. If the target file already exists, it is overwritten.

```csharp
public static bool FileWrite(string fileName, object JsonObject, System.Text.Encoding encoding)
```

Creates a new file, writes the bytes to the file, and then closes the file. If the target file already exists, it is overwritten.

### FileWriteAsync

```csharp
public static void FileWriteAsync(string file, byte[] data, Action<RemoteStorageFileWriteAsyncComplete_t, bool> callback)
```

```csharp
public static void FileWriteAsync(string file, string body, System.Text.Encoding encoding, Action<RemoteStorageFileWriteAsyncComplete_t, bool> callback)
```

```csharp
public static void FileWriteAsync(string fileName, object JsonObject, System.Text.Encoding encoding, Action<RemoteStorageFileWriteAsyncComplete_t, bool> callback)
```

Creates a new file and asynchronously writes the raw byte data to the Steam Cloud, and then closes the file. If the target file already exists, it is overwritten.

### FileWriteStreamCancel

```csharp
public static bool FileWriteStreamCancel(UGCFileWriteStreamHandle_t handle)
```

Cancels a file write stream that was started by FileWriteStreamOpen.

### FileWriteStreamClose

```csharp
public static bool FileWriteStreamClose(UGCFileWriteStreamHandle_t handle)
```

Closes a file write stream that was started by FileWriteStreamOpen.

### FileWriteStreamOpen

```csharp
public static UGCFileWriteStreamHandle_t FileWriteStreamOpen(string file)
```

Creates a new file output stream allowing you to stream out data to the Steam Cloud file in chunks. If the target file already exists, it is not overwritten until FileWriteStreamClose has been called.

To write data out to this stream you can use FileWriteStreamWriteChunk, and then to close or cancel you use FileWriteStreamClose and FileWriteStreamCancel respectively.

### FileWriteStreamWriteChunk

```csharp
public static bool FileWriteStreamWriteChunk(UGCFileWriteStreamHandle_t handle, byte[] data)
```

Writes a blob of data to the file write stream.

### GetCashedUGCCount

```csharp
public static int GetCachedUGCCount()
```

Undocumented, assumed to be depricated.

### GetCashedUGCHandles

```csharp
public static UGCHandle_t[] GetCashedUGCHandles()
```

Undocumented, assumed to be depricated.&#x20;

### GetFileCount

```csharp
public static int GetFileCount()
```

Gets the total number of local files synchronized by Steam Cloud.

### GetFiles

```csharp
public static RemoteStorageFile[] GetFiles()
```

Gets a collection containing information about all of the files stored on the Steam Cloud system

```csharp
public static RemoteStorageFile[] GetFiles(string extension)
```

Returns the subset of files found on the user's Steam Cloud that end with the speicifed value

### GetFileTimestamp

```csharp
public static DateTime GetFileTimestamp(string name)
```

Gets the specified file's last modified timestamp

### GetLocalFileChangeCount

```csharp
public static int GetLocalFileChangeCount()
```

Note: only applies to applications flagged as supporting dynamic Steam Cloud sync.

### GetLocalFileChange

```csharp
public static string GetLocalFileChange(int index, out ERemoteStorageLocalFileChange changeType, out ERemoteStorageFilePathType pathType)
```

Note: only applies to applications flagged as supporting dynamic Steam Cloud sync.

After calling GetLocalFileChangeCount, use this method to iterate over the changes. The changes described have already been made to local files. Your application should take appropriate action to reload state from disk, and possibly notify the user.

For example: The local system had been suspended, during which time the user played elsewhere and uploaded changes to the Steam Cloud. On resume, Steam downloads those changes to the local system before resuming the application. The application receives an RemoteStorageLocalFileChange\_t, and uses GetLocalFileChangeCount and GetLocalFileChange to iterate those changes. Depending on the application structure and the nature of the changes, the application could:

* Re-load game progress to resume at exactly the point where the user was when they exited the game on the other device
* Notify the user of any synchronized changes that don't require reloading

### GetQuota

```csharp
public static bool GetQuota(out ulong totalBytes, out ulong remainingBytes)
```

Gets the number of bytes available, and used on the users Steam Cloud storage.

### GetSyncPlatforms

```csharp
public static ERemoteStoragePlatform GetSyncPlatforms(string file)
```

Obtains the platforms that the specified file will synchronize to.

### GetUGCDetails

```csharp
public static bool GetUGCDetails(UGCHandle_t handle, out AppId_t appId, out string name, out int size, out CSteamID owner)
```

Undocumented, it is assumed to fetch the data about a UGC such as seen from the GetCashedUGCHandles

### GetUGCDownloadProgress

```csharp
public static bool GetUGCDownloadProgress(UGCHandle_t handle, out int downloaded, out int expected)
```

Undocumented, it is assumed to fetch the download state information for a UGC Handle as returned from the GetCashedUGCHandles

### SetSyncPlatfroms

```csharp
public static bool SetSyncPlatforms(string file, ERemoteStoragePlatform platform)
```

Allows you to specify which operating systems a file will be synchronized to.\
\
Use this if you have a multiplatform game but have data which is incompatible between platforms.\
\
Files default to [k\_ERemoteStoragePlatformAll](https://partner.steamgames.com/doc/api/ISteamRemoteStorage#k\_ERemoteStoragePlatformAll) when they are first created. You can use the bitwise OR operator, "|" to specify multiple platforms.

### UGCDownload

```csharp
public static void UGCDownload(UGCHandle_t handle, uint priority, Action<RemoteStorageDownloadUGCResult_t, bool> callback)
```

Undocumented, assumed to be deprecated.

### UGCDownloadToLocation

```csharp
public static void UGCDownloadToLocation(UGCHandle_t handle, string location, uint priority, Action<RemoteStorageDownloadUGCResult_t, bool> callback)
```

Undocumented, assumed to be deprecated.

### UGCRead

```csharp
public static byte[] UGCRead(UGCHandle_t handle)
```

Undocumented, assumed to be deprecated.
