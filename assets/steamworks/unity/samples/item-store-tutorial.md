# Item Store Tutorial

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More!"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

This scene is meant to be used in conjunction with the learning article [Item Store](../guides/microtransactions/item-store/). It provides a crude example of an in-game item store where the developer has defined each item's UI element and linked it with the related [Item Defintion](../scriptable-objects/item-definition.md).

![](<../../../../.gitbook/assets/image (162).png>)

### What do I learn?

1. Using [Item Defintion](../scriptable-objects/item-definition.md) to interact with the user's inventory.
2. Using [Item Definition](../scriptable-objects/item-definition.md) and Unity uGUI to represent a store item.
3. Responding to changes in the user's inventory.
4. How to access the Knowledge Base (where you are now)
5. How to access the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

## Objects

### Example Item Behaviour

This is a crude script serving as an example of how you might control a Unity UI object based on the information in a given Item Definition.

Using this we update a UI Text label indicating how many of the given item the user owns

We provide handlers for Start Purchase and Exchange buttons

and

We update the UI when the local user's inventory changes
