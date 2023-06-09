# Editor Coroutines

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../steam/steam.md">steam.md</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

As you may know by default coroutines don't work in the Unity editor.&#x20;

### Why?

StartCoroutine is part of GameObject and depends on the Update loop of the simulation. Unity has released a package that adds the feature into the Editor scripts but its "preview" and wonky at the moment ... and its pretty easy to do your self so this article will help with that.

## Approach

The approach is simple enough, we will register an event handler on Unity's `EditorApplication.update` event; this event gets called on update so will work like the GameObject update loop does ... mostly.

Next we will handle that event with our own little take on iterating coroutines, this means we will be tracking each coroutine and iterating over them all updating them as required on each "update" of the editor application.

Finally we need our own `StartCoroutine(IEnumerator handle)` method for the event handler to work on

### Solution

Now you could create a static class or another global solution to hold these methods but we tend to create these in each editor script such that debugging is a bit easier and scoped to each script on its own.&#x20;

The example I will show here assumes your creating this in your editor script as opposed to some global solution.

```csharp
private static List<IEnumerator> coroutines;

private static void StartCoroutine(IEnumerator handle)
{
    if (coroutines == null)
    {
        EditorApplication.update -= EditorUpdate;
        EditorApplication.update += EditorUpdate;
        coroutines = new List<IEnumerator>();
    }

    coroutines.Add(handle);
}

private static void EditorUpdate()
{
    List<IEnumerator> done = new List<IEnumerator>();

    if (coroutines != null)
    {
        foreach (var e in coroutines)
        {
            if (!e.MoveNext())
                done.Add(e);
            else
            {
                if (e.Current != null)
                    Debug.Log(e.Current.ToString());
            }
        }
    }

    foreach (var d in done)
        coroutines.Remove(d);
}
```

So lets walk through what each part does line by line

### Line 1

```csharp
private static List<IEnumerator> coroutines;
```

This is simply a storage point for our coroutines, we will be iterating over this list on each update to move it forward.

### Line 3

```csharp
private static void StartCoroutine(IEnumerator handle)
```

The StartCoroutine method, this is what we will call when we want to add a coroutine to be processed. This method does two important things for us.

1. If the coroutines collection is not initialized, initialize it and connect the update event
2. Add the handle passed in to our coroutines list

You will notice that when we register on the update event we first remove our selves then add our selves back ... why?

This insures that if we already had a handler on the event that we aren't duplicating it.

### Line 15

```csharp
private static void EditorUpdate()
```

EditorUpdate, this is the method we register to the EditorApplication update event, it will be called on each "frame" of the editor application. This method does three important things for us

1. It iterated over the list of coroutines calling MoveNext to advance them to the next yield statement.
2. It records any completed coroutines to a "done" list so we can remove them once the iteration is done.
3. It removes completed coroutines from the coroutines list

## How to Use

You can simply copy the code provided in the Approach section into your Editor script and then use coroutines as you would in Unity ... for example.

```csharp
[InitializeOnLoadMethod]
public static void CheckForSteamworksInstall()
{
    StartCoroutine(ValidateAndInstall());
}
```

Where ValidateAndInstall would be a method that returned an IEnumerator
