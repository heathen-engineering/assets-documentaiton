# 9 Item Store Tutorial

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction&#x20;

This scene is meant to be used in conjunciton with the learning article [Item Store](../core-concepts/inventory/item-store.md). It provides a crude example of an in-game item store where the developer has defined each item's UI element and linked it with the related [Item Defintion](../../objects/item-definition.md).

![](<../../../../.gitbook/assets/image (162).png>)

### What do I learn?

1. Using [Item Defintion](../../objects/item-definition.md) to interact with the user's inventory.
2. Using [Item Definition](../../objects/item-definition.md) and Unity uGUI to represent a store item.
3. Responding to changes in the user's inventory.
4. How to access the Knowledge Base (where you are now)
5. How to acces the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

## Objects

### Example Item Behaviour

This is a crude script serving as an example of how you might control a Unity UI object based on the informaiton in a given Item Defintion.

Using this we update a UI Text label indicating how many of the given item the user owns

We provide handlers for Start Purchase and Exchange buttons

and

We update the UI when the local user's inventory changes
