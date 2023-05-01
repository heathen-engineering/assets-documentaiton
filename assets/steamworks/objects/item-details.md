# Item Detail

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
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

