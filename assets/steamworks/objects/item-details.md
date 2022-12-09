# Item Detail

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct ItemDetail
```

Used by the [Inventory ](../api/inventory.md)interface and in the [Item Definition](../unity/scriptable-objects/item-definition.md) to represent instances of an item.

## Fields and Attributes

| Type                   | Name              | Comment                                          |
| ---------------------- | ----------------- | ------------------------------------------------ |
| SteamItemDetails\_t    | itemDetails       | The ID of the DLC                                |
| ItemProperty\[]        | properties        | Properties of the item                           |
| string                 | dynamicProperties | Dynamic properties set on the item               |
| ItemTag\[]             | tags              | tags applied to the item                         |
| SteamItemInstanceID\_t | ItemId            | The instance ID of the item                      |
| SteamItemDef\_t        | Definition        | the definition ID of the item                    |
| ushort                 | Quantity          | Quantity represented by the instnace of the item |
| ESteamItemFlags        | Flags             | <p>No Trade</p><p>Removed</p><p>Consumed</p>     |

