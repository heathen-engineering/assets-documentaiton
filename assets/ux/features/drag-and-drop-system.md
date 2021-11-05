---
description: Easy to use, drag and drop system for Unity 3D
---

# Drag and Drop System

## Introduction

{% hint style="info" %}
Available in UX [Complete](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)
{% endhint %}

The drag and drop system makes it easy to create drag-able, intractable elements and to define rules for drop points with no coding required. Consisting of 2 major features **Item** and **Container,** designers can quickly create spell bars, inventory systems and more without needing a single line of scripting.

![The Drag Item Componenet](<../../../.gitbook/assets/image (121).png>)

![The Drop Container Componenet](<../../../.gitbook/assets/image (122).png>)

## Configuration

### [Drag Item](../components/drag-item.md)

Drag and Drop Item objects are the objects that are to be dragged. The drag effect and drop effect and clear drop effect can be defined on the item.

![](<../../../.gitbook/assets/image (124).png>)

#### Home Container

This is the `RectTransform` that the item shold consider its "home" when using the `Return Home` **Clear Drop Effect**

**Proxy Prefab**

This is the prefab that will be used when using `Move Proxy` or `Leave Proxy` **Drag Effect**s

#### Drag Effect

This defines what should happen with the object when its dragged the following options are available:

{% hint style="info" %}
Examples of each of these are available in the included demo scenes
{% endhint %}

* Move Self\
  This indicates that the object its self should rise to the top of of the hierarchy and be moved under the mouse pointer.
* Move Clone\
  This indicates that the object should be used to instantiate a clone of its self, the clone will be moved not the original object.
* Move Proxy\
  This requires the **Proxy Prefab** field to be populated, when the drag operation starts the **Proxy Prefab** will be instantiated and moved under the cursor.
* Leave Proxy\
  This requires the **Proxy Prefab** field to be populated, when the drag operation starts the **Proxy Prefab** will be instantiated and left where the object started, the object will then be moved.

#### Clear Drop Effect

This defines what should happen when the drag operation is "dropped" outside of a defined container, options include

* Return Home\
  This requires the **Home Container** field to be set, when drop occurs outside of a defined container the item will be returned to the defined transform.
* Return Previous\
  This indicates that the object should be returned to the previous parent transform when its dropped anywhere other than a valid drop container.

#### Types

![](<../../../.gitbook/assets/image (123).png>)

This is a list of Drop Type references which discribe this particular item and are used by Drop Container to filter in or out items e.g. to define the rules of what can or cannot be dropped into a container.

### [Drop Containers](drag-and-drop-system.md#drop-containers)

Drop Containers are how we define valid drop points and defines the filter types and masking mode for the container.&#x20;

![](<../../../.gitbook/assets/image (125).png>)

#### Recieve Mode

Discribes how the item should be recieved, options include

* **Take**\
  This will cause the container to "take" the item e.g. become the items new parent. This is useful for inventory where you want to move an item from 1 slot to another or similar use cases.
* **Clone**\
  This will cause the container to "clone" the item e.g. to create a copy of the item and become that copy's parent. This is useful for spellbooks where you want to copy an item from the spellbook into a spellbar or similar use cases.

#### Must Be Empty

This rule simply rejects item drops if the container is already occupied.

#### Mask Mode

This discribes how the Filter Types should be tested, options include

* **No Conditions**\
  This means the filter should simply be ignored, this container will accept any item.
* **Allow Any Of**\
  This means the dropped item must have 1 or more of the **Filter Types** listed in its **Types** list.
* **Allow If All Of**\
  This means tthe dropped item must have all of the **Filter Types** listed in its **Types** list.
* **Disallow Any Of**\
  This means the dropped item will only be rejected if the item's **Types** list contiaines any of the entries found in the **Filter Types** list.
* **Disallow If All Of**\
  This means the dropped item will only be rejected if the item's **Types** list contians all of the entries found in the **Filter Types** list.

#### Filter Types

![](<../../../.gitbook/assets/image (126).png>)

This is the list of **Drop Types** the **Mask Mode** rule should be applied to when comparing against the Dropped Drag Item's **Types** field.

### Drop Type

Masks can be applied to items and containers, and allow the designer to filter in or out what can be dropped on a slot. To accomplish this designers can define Types which can be used by the system to define rules for drops.

![Highlights the Types list of Drop Types in the Drag Item component](<../../../.gitbook/assets/image (127).png>)

![Highlights the Filter Types list of Drop Types in teh Drop Contianer component](<../../../.gitbook/assets/image (128).png>)
