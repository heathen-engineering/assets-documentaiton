# Selection Manager

## Introduction

{% hint style="info" %}
Part of the [Selection System](../learning/core-concepts/selection-system.md) of the UX Complete asset
{% endhint %}

This component simply exposes the selection changed event to the Unity Inspector and a selection of the common selection funcitons.

{% hint style="success" %}
Selection Manager is a .NET IColleciton of SelectableObjects ... this means you can iterate over it to iterate over the selected objects



```csharp
foreach(var selected in selectionManager)
{
    Debug.Log(selected.name + " is selected");
}
```
{% endhint %}

## Definition

### Fields and Attributes

<table><thead><tr><th width="150">Type</th><th width="150">Name</th><th width="370.2">Notes</th></tr></thead><tbody><tr><td>int</td><td>Count</td><td>Gets the count of currently selected objects</td></tr><tr><td>bool</td><td>IsReadOnly</td><td>Always returns true</td></tr></tbody></table>

### Events

#### Selection Changed

Occurs when the list of selected object's changes

### Funcitons

{% hint style="warning" %}
This simply operates the [API.Selection](../api/selection.md) interface. The interface its self has far more useful funcitons such as searching of selected objects and more.



You are strongly encuraged to use [API.Selection](../api/selection.md) directly.
{% endhint %}

#### Add

Adds the object to the selection

#### Add Range

Adds multiple objects to the selection

#### Remove

Removes an object from selection

#### Remove All

Removes all matching items from the selection

#### Clear

Clears all items from the selection

#### Contains

Returns true if the indicated item is in the selection

#### Copy To

Copies the selection to a target array

#### Get Enumerator

Used to iterate over the selected items
