# Remote Storage File



<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
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

