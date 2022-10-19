# Item Detail

## Definition

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

