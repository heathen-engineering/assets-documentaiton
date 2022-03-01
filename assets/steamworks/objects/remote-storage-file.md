# Remote Storage File

## Definition

```csharp
public struct RemoteStorageFile
```

Used by the [Remote Storage](../api/remotestorage.client.md) interface to represent a file located on the Steam Remote Stroage system.

### Fields and Attributes

| Type     | Name      | Comment                              |
| -------- | --------- | ------------------------------------ |
| string   | name      | The full name of the file on Steam   |
| int      | size      | The size in bytes                    |
| DateTime | timestamp | The current time stamp for this file |

