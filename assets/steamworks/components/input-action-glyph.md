# Input Action Glyph

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction

The Input action glyph simplifies display of a simple single input image for a given action. This tool sets the first glyph image mapped to this action to the attached RawImage texture.

## Definition

## Fields and Attributes

| Type                                                        | Name   | Comments                                                                                    |
| ----------------------------------------------------------- | ------ | ------------------------------------------------------------------------------------------- |
| [InputActionSet](../objects/input-action-set.md)            | set    | <p>The set the action is a member of.</p><p>Set this value or Layer value but not both.</p> |
| [InputActionSetLayer](../objects/input-action-set-layer.md) | layer  | <p>The layer the action is a member of.</p><p>Set this value or Set value but not both.</p> |
| [InputAction](../objects/input-action.md)                   | action | The action to fetch the glyph for                                                           |

## Methods

### Refresh Image

```csharp
public void RefreshImage();
```

Refreshes the image mapped to this action. This is automatically called on Start and OnEnable but can be manually refreshed as needed.
