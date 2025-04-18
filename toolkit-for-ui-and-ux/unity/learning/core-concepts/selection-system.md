---
description: Getting to know the Heathen selection system
---

# Selection System

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
Available in UX [Complete](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)
{% endhint %}

UX provides an easy to use, flexible, searchable multi-select system. Read more about the [API.Selection](../../api/selection.md) interface in its API article.

## Concepts

### [Selectable Object](../../components/selectable-object.md)

A selectable object is simply any game object which includes the [Selectable Object](../../components/selectable-object.md) component. This component exposes the [Scriptable Tag](../../../../assets/system-core/scriptable-tags.md) system, a selection changed event and provides easy access to check for and change the selection state of the object its attached to.

[Selectable Objects](../../components/selectable-object.md) at start will register them selves with the [API.Selection](../../api/selection.md) interface and deregister them selves on destroy. This means you can search for selectable objects in a more efficient manner than simply searching all game objects. The API.Selection interface also stores a collection of the currently selected Selectable Objects. You can use the API.Selection interface to search all Selectable Objects or limit your search to only those that are selected.

### Searchable

Why search?

This single selection system can handle all selectable things regardless of type and use however your various game systems likely need to understand what is selected or at least what types of things are selected, hence the search feature.

Imagine your creating an RTS, you have various things that can be selected including buildings, resource nodes and of course units, units have various types and categories such as naval, air, land, infantry, calvary, artillery.

You can now let your users do a simple box selection and register all contained selectable as selected. Your unit command system can then search getting back only those that are units and can be commanded.

```csharp
var results = API.Selection.GetAllSelected(Unit);
```

results now contains all of the selected units, you can search for multiple tags, you can return all matching selected or just the first and you can also search all selectable rather or not they are selected.

For example many RTS games let the user press a single button to select all workers

```csharp
var results = API.Selection.FindAll(Workers);
```

Tags can be added and removed at run time based on state ... imagine then that we added the Available tag to our workers when they where not doing anything and removed it when they where

```csharp
var results = API.Selection.FindAll(Workers, Available);
```

Now we have a list of all the idle workers and could simply select them all

```csharp
foreach(var result in results)
    result.IsSelected = true;
```

These are just a few simple examples of what can be done with such a flexible searchable selection system
