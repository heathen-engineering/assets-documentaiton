---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Item Store Tutorial

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This scene is meant to be used in conjunction with the learning article [Item Store](../../../steam/inventory/microtransactions/item-store/). It provides a crude example of an in-game item store where the developer has defined each item's UI element and linked it with the related [Item Definition](../scriptable-objects/item-definition.md).

<figure><img src="../../../.gitbook/assets/image (13) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The scene requires additional configuration in your Steam Developer Portal and a basic understanding of the [Steam Inventory](../../../company/steam/steamworks/inventory/) system to use properly.

## Objects

### Example Item Behaviour

This is a crude script serving as an example of how you might control a Unity UI object based on the information in a given Item Definition.

Using this we update a UI Text label indicating how many of the given item the user owns

We provide handlers for Start Purchase and Exchange buttons

and

We update the UI when the local user's inventory changes
