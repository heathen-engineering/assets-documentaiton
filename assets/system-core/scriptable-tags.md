---
description: Getting to grips with the scriptable tag concept
---

# Scriptable Tags

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

```csharp
public List<ScriptableObject> tags;
```

A scriptable tag is simply a scriptable object, it be absolutly any scriptable object at all. Scriptable Tags are usually used by systems such as the Selection System and Drag and Drop Systems to understand groupings or types of things; for example, you can configure the selection system to only select objects with the PlayerGroup tag ... PlayerGroup in this example is a scriptable object, it doesn't matter what kind of scriptable object; its just a way for the system to understand that it should only accept a selection request from Selectable Objects that contain PlayerGroup in there "tags" list.

This system works similar to Unity's Tag system only in the case of Scriptable Tags an object can have many tags not just 1.

### Scriptable Tag&#x20;

The UX system includes a special Scriptable Object type called Scriptable Tag. Scriptable Tag is an empty Scriptable Object, that is, its a Scriptable Object with no logic and no fields, it exists only to create unique Scriptable Objects in your asset database for use with the Scriptable Tag system such as seen on the [Selectable System](../../toolkit-for-ui-and-ux/unity/learning/core-concepts/selection-system.md) and [Drag and Drop Systems](../../toolkit-for-ui-and-ux/unity/learning/core-concepts/drag-and-drop-system.md).

```csharp
public class ScriptableTag : ScriptableObject
{}
```

## Using Tags

Scriptable Tags are used by the Selectable System and the Drag and Drop System but can be used in your own game logic just as easily. There are many uses for tag systems in just about any sort of process or system, the following is just one use case common to many types of games.

### Friend or Foe System

FoF or Friend or Foe systems are common place in many game types and in its simplest form is just a way for your system to understand what should or shouldn't be considered friend or foe be it a MOB or unit, etc. Many games will use Unity's built in Tag system for this however that has a number of issues, in particular its a string comparison so prone typos and not exsactly friendly to changes in code.

The Selectable Tag approch is an object reference so completly tollerent to name changes and more efficent in comparion than string to string. Selectable Tags can also be generated at run time and objects can have multiple tags making it easier to simulate multi-faction systems and similar.

#### Hypothetical

Lets assume we have a natural mob perhaps a dog, as a dog it may be friendly to dogs that belong to the same pack or area, its probably hostile to cats and postmen but generally friendly to humans at least the ones that are part of this area.

Considering the above we can see that we have a number of tags sugested here including

Tags for mob type

* Cat
* Dog
* Human

Tags for area

* Village 1
* Village 2
* Wilderness
* Unknown

We can now store these tags on all of our mobs

```csharp
public class Mob : MonoBehaviour
{
    public List<ScriptableObject> tags;
}
```

so if we where to spawn a new dog we might add the Dog and Village 1 tags to it spawn. When the dog checks for targets in range something most AI systems do at various points it can simply check for all Mobs in a given radius. Next it needs to know what to do with each mob, so we can perform checks such as.

```csharp
foreach(var mob in mobsInRange)
{
    if(mob.tags.Contains(catTag)
        || ( mob.tags.Contains(dogTag) && mob.tags.Contains(village2tag))
        {
            // We dont like cats at all or dogs from village 2 so go chase it
        }
}
```
