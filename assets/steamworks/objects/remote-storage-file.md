# Remote Storage File

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct RemoteStorageFile
```

Used by the [Remote Storage](../api/remote-storage.md) interface to represent a file located on the Steam Remote Stroage system.

### Fields and Attributes

| Type     | Name      | Comment                              |
| -------- | --------- | ------------------------------------ |
| string   | name      | The full name of the file on Steam   |
| int      | size      | The size in bytes                    |
| DateTime | timestamp | The current time stamp for this file |

