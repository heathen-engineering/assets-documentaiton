# DLC Data

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct DlcData
```

Used by the App interface to return general DLC information. In general using the [Downloadable Content Object](../unity/scriptable-objects/downloadable-content-object.md) is more effective.

## Fields and Attributes

| Type     | Name      | Comment                     |
| -------- | --------- | --------------------------- |
| AppId\_t | AppId     | The ID of the DLC           |
| bool     | Available | Is it available             |
| string   | Name      | The display name of the DLC |
