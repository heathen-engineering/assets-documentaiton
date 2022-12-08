# Workshop Item Data

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Used with the User Generated Content interface for 1 line creation of workshop items

## Definition

```csharp
public struct WorkshopItemData
```

Used with the User Generated Content interface for 1 line creation of workshop items.

### Fields and Attributes

| Type                                                                    | Name             | Comment                                                                                                                                              |
| ----------------------------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| AppId\_t                                                                | appId            | <p>Required</p><p>The of the inteded consumer app</p>                                                                                                |
| string                                                                  | title            | <p>Required</p><p>The title of the item</p>                                                                                                          |
| string                                                                  | description      | <p>Required</p><p>The description of the item</p>                                                                                                    |
| string                                                                  | contentFolder    | <p>Required</p><p>A valid folder path to the folder containing the content that will be uploaded to Steam</p>                                        |
| string                                                                  | previewImageFile | <p>Required</p><p>A valid file path to a JPG or PNG image file less than 1mb in size and to be uploaded to Steam as the items main preview image</p> |
| string                                                                  | metadata         | <p>Optional</p><p>Metadata to be attached to the item created</p>                                                                                    |
| [WorkshopItemPreviewFile](../objects/workshop-item-preview-file.md)\[]  | previewFiles     | <p>Optional</p><p>Additional item preview files</p>                                                                                                  |
| string\[]                                                               | youTubeIds       | <p>Optional</p><p>Preview videos, these must be valid YouTube video IDs</p>                                                                          |
| string\[]                                                               | tags             | <p>Optional</p><p>A list of tags to add to the item</p>                                                                                              |
| [WrokshopItemKeyValueTag](../objects/workshop-item-key-value-tag.md)\[] | keyValueTags     | <p>Optional</p><p>A list of key value tags to add to the item</p>                                                                                    |

