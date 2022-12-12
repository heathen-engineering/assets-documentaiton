---
description: Flexable, searchable multi-select system
---

# Selection

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public static class API.Selection
```

Make game objects selectable and searchable with an easy to use and simple interface.

### What can it do?

* Make any game object selectable
* Handle multi-select e.g. having more than 1 item selected at a time
* Handles selectable types using a simple but robust tag system
* Search through all selected objects
* Search through all available selectables rather they are selected or not&#x20;

## Events

### Selection Changed

Occurs when the selection state changes and expresses the set of added and removed selectables.

{% hint style="info" %}
Each selectable has its own selection changed event which is raised when that item is added to or removed from the selection.
{% endhint %}

## Concepts

### Selectables

A selectable is any game object which includes a Selectable Object component. These objects will register and deregister them selves from the selection system on create and destroy respectivly and can be used to search selections, available selectablles and to get specific selected objects.

A core concept at use by the selection system is the Heathen Tag system. This allows you to mark up selectables with specific tags. You can use these tags with the selection system to get the set of all selected objects which have a given tag or tags.

#### Example

Imagin we have the following tags

* UnitTag
* InfantryTag
* CalvaryTag
* AirTag
* SeaTag

In this case all of our units would be selectables and would have at least 2 tags being Unit and whatever type of Unit they where such as Infantry. The player can now select a group of units regardless of what type they may be and we can get the subset of the selected units that match a given type e.g.&#x20;

```csharp
var selectedInfantry = API.Selection.GetAllSelected(UnitTag, InfantryTag);
```

or we could simply fetch all selected Units

```csharp
var selectedUnits = API.Selection.GetAllSelected(UnitTag);
```

This concept can be used with any gameobject including world objects and UI, anything that you can attach a Selectable Object component to.

## How To

{% hint style="info" %}
An object must have the Selectable Object component in order to be selectable. Search features require the use of [Heathen's Tag](../../system-core/scriptable-tags.md) system.
{% endhint %}

### Select Objects

How you determin that the user wants to select a given object is wholly up to you. You can use mouse input, keyboard, or anything you like. The actual point of selection is when you add that object to the current selection and you can do so in a few ways.

#### To Single Select the object

In this use case you want to deselect all other objects and select just this object

```csharp
API.Selection.Clear();
API.Selection.Add(obj);
```

#### Add to existing selection

In this use case you want to add an object to the current set of selected things

```csharp
API.Selection.Add(obj);
```

#### Add multiple items to the current selection

In this use case you want to add a range of items to the current selection

```csharp
API.Selection.AddRange(items);
```

or

```csharp
API.Selection.AddRange(item1, item2, item3, etc);
```

{% hint style="info" %}
you can also use the Selectable Object componenet to set the object selected or not

```csharp
mySelectable.IsSelected = true;
```
{% endhint %}

### Get Selected

The Selection interface gives you easy to use and powerful tools for fetching objects that are selected or even objects that are selectable rather they are currently selected or not.

#### Simply get all selected

Simple and to the point, this will return a copy of the selected array.

{% hint style="info" %}
This yields a copy of the selection

As such removing or adding items to this colleciton has no effect on the selection. It also however means that you can iterate over this collection and modify the selection without breaking the enumeration.
{% endhint %}

```csharp
var results = API.Selection.GetSelected();
```

#### Get First Selected

This search tool will return the first selectable found that matches the supplied predicate. You can search with scriptable tags, unity tag or by a custom predicate, some examples follow.

```csharp
var result = API.Selection.GetFristSelected(UnitTag, InfantryTag);
```

```csharp
var result = API.Selection.GetFirstSelected(desiredTags);
```

```csharp
var result = API.Selection.GetFirstSelected("unity tags work to");
```

```csharp
var result = API.Selection.GetFirstSelected(p => p.name == "Something");
```

#### Get All Selected

The Get First Selected feature set will return 1 selectable object being the first found that matches the provided predicate. The Get All Selected has the same capabilities but returns all selected objects that match the predicate.

```csharp
var results = API.Selection.GetAllSelected(UnitTag);
```

As noted you can use all forms of predicate including a custom predicate.

### Find Selectables

#### Get all selectables

You can simply return all selectables simply

{% hint style="info" %}
This returns a copy of the selectables.&#x20;

As such modifying the collection does not effect the registered selectables.
{% endhint %}

```csharp
results = API.Selection.GetSelectables();
```

You can search all selectables registered to the system rather or not they are currently selected. This works much like the Get First Selected and Get All Selected but operates on all selectables not just those that are currently selected.

#### Find

Find will return the first selectable that matches the predicate. You can use any predicate you want with built in support for scriptable tags and Unity tags but also able to use custom predicates.

```csharp
var result = API.Selection.Find(UnitTag);
```

To find all selectables that match your predicate use

```csharp
var results = API.Selection.FindAll(UnitTag);
```

