# Workshop Item Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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

