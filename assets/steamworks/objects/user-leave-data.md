# User Leave Data

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct UserLeaveData
```

Used by the [Clans ](../api/clans.md)interface indicating a user leaving a target chat

### Fields and Attributes

| Type     | Name    | Comment     |
| -------- | ------- | ----------- |
| ChatRoom | room    | The room    |
| UserData | user    | The user    |
| bool     | kicked  | Was kicked? |
| bool     | dropped | Droped out? |

