# Workshop Item Data

## Introduction

Used with the User Generated Content interface for 1 line creation of workshop items

## Definition

```csharp
public struct WorkshopItemData
```

Used with the User Generated Content interface for 1 line creation of workshop items.

### Fields and Attributes

| Type                                                         | Name             | Comment                                                                                                                                              |
| ------------------------------------------------------------ | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| AppId\_t                                                     | appId            | <p>Required</p><p>The of the inteded consumer app</p>                                                                                                |
| string                                                       | title            | <p>Required</p><p>The title of the item</p>                                                                                                          |
| string                                                       | description      | <p>Required</p><p>The description of the item</p>                                                                                                    |
| string                                                       | contentFolder    | <p>Required</p><p>A valid folder path to the folder containing the content that will be uploaded to Steam</p>                                        |
| string                                                       | previewImageFile | <p>Required</p><p>A valid file path to a JPG or PNG image file less than 1mb in size and to be uploaded to Steam as the items main preview image</p> |
| string                                                       | metadata         | <p>Optional</p><p>Metadata to be attached to the item created</p>                                                                                    |
| [WorkshopItemPreviewFile](workshop-item-preview-file.md)\[]  | previewFiles     | <p>Optional</p><p>Additional item preview files</p>                                                                                                  |
| string\[]                                                    | youTubeIds       | <p>Optional</p><p>Preview videos, these must be valid YouTube video IDs</p>                                                                          |
| string\[]                                                    | tags             | <p>Optional</p><p>A list of tags to add to the item</p>                                                                                              |
| [WrokshopItemKeyValueTag](workshop-item-key-value-tag.md)\[] | keyValueTags     | <p>Optional</p><p>A list of key value tags to add to the item</p>                                                                                    |

