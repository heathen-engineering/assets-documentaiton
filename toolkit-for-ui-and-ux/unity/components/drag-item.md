# Drag Item

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

To be attached to an object that can be dragged, meant for use with the Drag and Drop system. The intent of this componenet is that you add it to the Unity Engine UI object you want to be draggable, it could represent a spell, inventory item, etc.

You can use the static members listed below to understand the state of the drag and drop system as a whole.

### Drag Object

The object currently being dragged if any

```csharp
public static DragItem dragObject;
```

## Concepts

### Types

You will notice the Drag Item has a `Types` field which takes any kind of scriptable object you would like to place in it. This operates much like a "tag" system and in fact we provide a scriptable object `ScriptableTag` that contains no data and is meant for exsactly this sort of use. You can read more about [ScriptableTag here](../../../assets/system-core/scriptable-tags.md).

#### Example

Lets assume we are using Drag and Drop for an ability bar system. Lets then assume we have weapon and spell abilities which can be "normal" or "ultimate" and that 1 of our slots the "ultimate" slot can take any normal ability or ultimate ability but that normal slots cannot take ultimate abilities.

We would then create scriptable objects as such

* Ability
* Weapon
* Spell
* Ultimate

We would add all of the scriptable objects to our Drop Item that matched, so all of them would get "Ability", all of the weapon abilities but not the spells would get "Weapon", all the spells but not weapon abilities would get "Spell" and so on.

We can now configure the Drop Containers accordingly. That is we can indicate that they take Abilities and which one allows for Ultimate or excludes Ultimate. You can read more about [Drop Container](drop-container.md) and its filter in its article.

You can see a working example of this sort of conditional limits in the examples. In our examples we have slots and items that have 2 attributes color and number. some slots have just 1 attribute some have both some have none e.g. can take any item. This system lets you insure your users cant drag abilities to inventory slots, cant put a helmet on there feet, etc.

## Definition

### Fields and Attributes

| Type                                                   | Name            | Notes                                                                           |
| ------------------------------------------------------ | --------------- | ------------------------------------------------------------------------------- |
| Transform                                              | homeContainer   | The home container for this object                                              |
| GameObject                                             | proxyPrefab     | The proxy to be used if any. This is used if the Move Effect type is Move Proxy |
| [DragEffect](../enums/drag-effect.md)                  | dragEffect      | What effect should be applied on drag                                           |
| [ClearDropBehaviour](../enums/clear-drop-behaviour.md) | clearDropEffect | What should happen on a clear drop                                              |
| List\<ScriptableObject>                                | types           | Used as a multi-tag system for defining drop rules on containers                |

### Events

#### Drag Started

Occurs when the drag operation starts

#### Drop Accepted

Occurs when the drop operation is accepted

#### Drop Cancled

Occurs when the drop operation is cancled
