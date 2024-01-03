# Drag and Drop (Spell Bar Example)

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (565).png>)

This scene demonstrates tags and rules similar to the [Drag and Drop (Inventory Exmaple)](drag-and-drop-inventory-example.md) scene with the only signifigant difference being that the behvaiours are set up to emulate a spell book or ability bar.

## What do I learn?

1. Setting up code free drag and drop
2. Setting up [drop containers](../../components/drop-container.md)
3. Setting up [drag items](../../components/drag-item.md)
4. Using [Scriptable Tags](../../../system-core/scriptable-tags.md) to defaine item types and cotrol drop rules
5. Settting up drop rules on drop containers
6. How to access the Knowledge Base (where you are now)
7. How to access the support [Discord ](https://discord.gg/6X3xrRc)
8. How to leave a review 😉

## Objects

### Types

The "Types" and "Filter Types" fields of Drag Item and Drop Container respectivly take Scriptable Objects. That is we use Scriptable Objects as unique identifiers to power our filtering system. This is better than simple strings in that comparing two Scriptable Objects is faster and less error prone than comparing two strings. We use the same system in the [Heathen Behaviour](../../../system-core/scriptable-tags.md) to tag behaviours.

You can use any Scriptable Object you would like to represent a type. We have create a simple empty Scriptable Object called a [Scriptable Tag](../../../system-core/scriptable-tags.md) which we use in this scene. [Scriptable Tag](../../../system-core/scriptable-tags.md) has no long and not data it simply represents a unique referencable identifier.

### Spells

These are Drag and Drop items configured with types similar to the Items in the Inventory exmaple.

![](<../../../../.gitbook/assets/image (266).png>)

### Slots

These are Drop Containers configured with Type Filters similar to the slots in the Inventory example.

![](<../../../../.gitbook/assets/image (418).png>)
