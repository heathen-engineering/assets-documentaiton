# Item Detail

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public struct ItemDetail
```

Used by the [Inventory ](../api/inventory.client.md)interface and in the [Item Definition](../../unity/scriptable-objects/item-definition.md) to represent instances of an item.

## Fields and Attributes

<table><thead><tr><th width="234.2444989075424">Type</th><th width="178.8468268360739">Name</th><th width="375.82373346952215">Comment</th></tr></thead><tbody><tr><td>SteamItemDetails_t</td><td>itemDetails</td><td>The ID of the DLC</td></tr><tr><td>ItemProperty[]</td><td>properties</td><td>Properties of the item</td></tr><tr><td>string</td><td>dynamicProperties</td><td>Dynamic properties set on the item</td></tr><tr><td>ItemTag[]</td><td>tags</td><td>tags applied to the item</td></tr><tr><td>SteamItemInstanceID_t</td><td>ItemId</td><td>The instance ID of the item</td></tr><tr><td>SteamItemDef_t</td><td>Definition</td><td>the definition ID of the item</td></tr><tr><td>ushort</td><td>Quantity</td><td>Quantity represented by the instnace of the item</td></tr><tr><td>ESteamItemFlags</td><td>Flags</td><td><p>No Trade</p><p>Removed</p><p>Consumed</p></td></tr></tbody></table>

