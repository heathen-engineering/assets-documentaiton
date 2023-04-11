---
description: How to work with Unity's Package Manager in editor scripts
---

# Package Manger in C\#

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/steam/">Guides and Tutorials</a></td><td><a href="../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

Package Manager, while its not great it is what Unity Technology has moved to and it does give us what we need in terms of a means to query and see what is installed and detect the version that is installed.

### How?

```csharp
using UnityEditor.PackageManager;
using UnityEditor.PackageManager.Requests;
```

These two namespaces give us everything we need to query what packages are installed and even kick off remove, update or installs operations.

{% hint style="info" %}
Package Manager processes are asynchronous so you will need a means to handle that. You can use background workers or other methods but we tend to prefer [Coroutines ](editor-coroutines.md)as they are familiar to other Unity developers and also let us work with things that aren't thread safe.&#x20;



[Want to know how to use Editor Coroutines? read this article!](editor-coroutines.md)
{% endhint %}

## Listing Packages

```csharp
var listProc = Client.List();

while (!listProc.IsCompleted)
    yield return null;
```

The above code will use the PackageManager.Client to list all installed packages for you. Once the process is completed you should check for success and if so iterate over the results to find what your looking for.

```csharp
bool isInstalled = false;
if (listProc.Status == StatusCode.Success)
{
    var systemCore = listProc.Result.FirstOrDefault(p => p.name == "com.heathen.systemcore");
    if(systemCore != default)
    {
        isInstalled = true;
        Debug.Log("System Core Version: " + systemCore.version + " is installed");
    }
}
else
    Debug.LogError("Failed to list Package Manager packages: " + listProc.Error.message);
```

The above example is a crude, non-practical example. Above we are simply searching for an installed package whose name matches System Core's package then setting a bool to true if its there and debug logging its version string.

In reality you would want to for example compare the version with a minimal require version, or perhaps you only care if its not installed so really a&#x20;

```csharp
if(!listProc.Result.Any(p => p.name == "com.heathen.systemcore"))
{
    //We need to install it
}
```

would be more practice for you

## Installing/Updating Packages

{% hint style="warning" %}
Installing or updating packages will cause the Unity editor to recompile and thus reload scripts, thus triggering any processes to fire again … you need to uses [`SessionState` ](https://docs.unity3d.com/ScriptReference/SessionState.html)parameters that can survive this to manage state.
{% endhint %}

```csharp
var sysProc = Client.Add("https://github.com/heathen-engineering/SystemCore.git?path=/com.heathen.systemcore");
```

The above example uses the PackageManager.Client to add Heathen's System Core tot he manifest. As with listing this is Asynchronous so you need to handle that for example:

```csharp
while (sysProc.Status == StatusCode.InProgress)
    yield return null;
```

This would simply yield until complete, this is an example only you could have timeout timers running or similar but it illustrates the point of waiting for that async process to complete.

Finally check for errors and handle them accordingly

```csharp
if (sysProc.Status == StatusCode.Failure)
    Debug.LogError("PackageManager's System Core install failed, Error Message: " + sysProc.Error.message);
else if (sysProc.Status == StatusCode.Success)
    Debug.Log("System Core " + sysProc.Result.version + " installation complete");
```

The above code will print the error if any, if none it will print the version that was installed.

## Removing Packages
