# Drag and Drop (Inventory Example)

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (174) (1) (1).png>)

This scene gives a more practice example of code free drag and drop and shows how to use tags and rules to control what can be draged to where. In this scene each drag item is idetified with a color and a number, each slot has either or both a number and a color.&#x20;

Colorless slots can take any color

Numberless slots can take any number

Red slots can only take red blocks

Numbered slots can  only take blocks of the same number

Using color and number is simply done to keep it simple and abstract you can greate any number and complex of tags you like (Weapon, Armour, Left Glove, Basic Attack, etc.) and use that to control drop behaviour.

## What do I learn?

1. Setting up code free drag and drop
2. Setting up [drop containers](../../components/drop-container.md)
3. Setting up [drag items](../../components/drag-item.md)
4. Using [Scriptable Tags](../../../../assets/system-core/scriptable-tags.md) to defaine item types and cotrol drop rules
5. Settting up drop rules on drop containers
6. How to access the Knowledge Base (where you are now)
7. How to access the support [Discord ](https://discord.gg/6X3xrRc)
8. How to leave a review 😉

## Objects

### Types

The "Types" and "Filter Types" fields of Drag Item and Drop Container respectivly take Scriptable Objects. That is we use Scriptable Objects as unique identifiers to power our filtering system. This is better than simple strings in that comparing two Scriptable Objects is faster and less error prone than comparing two strings. We use the same system in the [Heathen Behaviour](../../../../assets/system-core/scriptable-tags.md) to tag behaviours.

You can use any Scriptable Object you would like to represent a type. We have create a simple empty Scriptable Object called a [Scriptable Tag](../../../../assets/system-core/scriptable-tags.md) which we use in this scene. [Scriptable Tag](../../../../assets/system-core/scriptable-tags.md) has no long and not data it simply represents a unique referencable identifier.

### Items

You will find 4 items configured under the \
Canvas > Background > Inventory \
Game object. Each item has two "types" assigned. A type is simply a scriptable object and is used like a tag by the drop rules e.g. does the item have this tag, does that allow it or forbid it.

![](<../../../../.gitbook/assets/image (163) (1) (1) (1) (1).png>)

### Slots / Containers

In the middle of the screen you will see 8 slots/containers located under the \
Canvas > Background > Simple Slots \
and\
Canvas > Background > Complex Slots\
Game objects respetivly, each slot is configured with "Filter Types" and "Mask Mode" which effects what items can and cannot be droped on it.

![](<../../../../.gitbook/assets/image (172) (1).png>)
