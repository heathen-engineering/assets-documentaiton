# Item Detail

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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

