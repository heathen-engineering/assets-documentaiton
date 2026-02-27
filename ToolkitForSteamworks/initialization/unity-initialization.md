# Unity Initialization

{% hint style="info" %}
Legacy worked a bit differently for initialisation ... \
See [Legacy Getting Started](https://kb.heathen.group/old-kb/old-toolkit-for-steamworks/unity/legacy/quick-start-guide) for more info.
{% endhint %}

{% hint style="success" %}
1st and foremost ... if you have SteamManager.cs in your project, remove it.

\
That script should not be used at all; it is not part of Heathen's Toolkit, and it was not meant to be dragged and dropped into a production project in the first place.
{% endhint %}

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><h3>Pure Code</h3></td><td><ul><li>Doesn't require a GameObject</li><li>No ScriptableObject</li><li>Pure C#</li></ul></td><td><a href="../.gitbook/assets/image (260).png">image (260).png</a></td><td><a href="unity-initialization.md#pure-code-1">#pure-code-1</a></td></tr><tr><td><h3>Code Free</h3></td><td><ul><li>Set your desired settings.</li><li>Add a component to the game object. </li><li>Done!</li></ul></td><td><a href="../.gitbook/assets/image (258).png">image (258).png</a></td><td><a href="unity-initialization.md#component">#component</a></td></tr></tbody></table>

## Pure Code

You do NOT require any GameObjects to make Steamworks run. You can simply call the [generated wrapper](../configuration/unity-configuration.md#generate-wrapper).

```csharp
SteamTools.Interface.Initialise();
```

### Ready Check

You can check if the interface is ready to use by using the Interface class

```csharp
private void Start()
{
    if (SteamTools.Interface.IsReady)
    {
        // Ready to go
    }
    else
    {
        // Not ready yet, listen for On Ready
        SteamTools.Interface.OnReady += Interface_OnReady;
    }
}

private void Interface_OnReady()
{
    // Ready now
}
```

Or you can use the "When Ready" feature.

```csharp
private void Start()
{
    SteamTools.Interface.WhenReady(Interface_OnReady);
}

private void Interface_OnReady()
{
    // Ready Now
}
```

### Debugging

To enable debugging from code, you can set:

```csharp
SteamTools.Interface.IsDebugging = true;
```

This will cause it to be more verbose about things. In general, you would set this before you initialise, so you can get more verbose initialisation steps as well.

## Code Free

If you need a code-free solution, we provide you with a component script which will initialise the Steamworks SDK for you based on your configured settings.

<figure><img src="../.gitbook/assets/image (396).png" alt=""><figcaption></figcaption></figure>

There are no settings needed; that is all handled by your [configuration](../configuration/unity-configuration.md). You do not need to mark this object Do Not Destroy, It exists to do nothing more than call

```csharp
SteamTools.Interface.Initialise();
```
