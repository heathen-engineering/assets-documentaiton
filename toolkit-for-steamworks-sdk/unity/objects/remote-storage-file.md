---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

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

Used by the [Remote Storage](../api/remotestorage.client.md) interface to represent a file located on the Steam Remote Stroage system.

### Fields and Attributes

<table><thead><tr><th width="187.56643368118847">Type</th><th width="173.82668241105068">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>string</td><td>name</td><td>The full name of the file on Steam</td></tr><tr><td>int</td><td>size</td><td>The size in bytes</td></tr><tr><td>DateTime</td><td>timestamp</td><td>The current time stamp for this file</td></tr></tbody></table>

