# Drop Container

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
Part of the [Drag and Drop System](../learning/core-concepts/drag-and-drop-system.md) of the UX Complete asset
{% endhint %}

A place to drop your drag items. You can use this component to define drop rules restricting the types of Drop Items that can be accepted by this container.

The intended use is that you place this on a Unity Engine UI object e.g. a RectTransform that acts as a slot or drop point for whatever your drag items are.

## Concepts

### Filter Types & Mask Mode

Drop Containers and Drag Items can specify "types" on them. These types are simply Scriptable Objects that work much like tags. Depending on the Mask Mode you choose to apply you can cause a Drop Container to accept or reject specific items.

For example you can insure that a user cant equip a helmet to its feet but that both boots and helmits can be in bag slots. Working examples of complex situations such as inventory to equipment slots, speel book to action bar and more are shown in the example scenes.

## Definition

### Fields and Attributes

| Type                                    | Name        | Notes                                                                                                                             |
| --------------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------- |
| bool                                    | HasItem     | true if the container is occupied                                                                                                 |
| [DragItem](drag-item.md)                | Item        | the item contained if any                                                                                                         |
| [RecieveMode](../enums/recieve-mode.md) | recieveMode | What should this container do when an item is dropped and accepted e.g. Take or Clone                                             |
| bool                                    | mustBeEmpty | Will this container reject incoming items if its already occupied                                                                 |
| [MaskMode](../enums/mask-mode.md)       | maskMode    | What filtering rules should be used if any                                                                                        |
| List\<ScriptableObject>                 | filterTypes | The mask values to be used e.g. items will be tested to see if they contain required types or do not contain excluded types, etc. |
