---
description: Creating assets based on System Core
---

# Asset Developers

## Overview

So you want to use System Core as a dependency for your assets? That's great!

{% hint style="success" %}
Yes the MIT license with its common clause does allow you to create assets that are dependent on System Core. The common clause simply aims to prevent people from copying or deriving from System Core code to release a competitor to System Core paid or otherwise.



If you would like to make a better System Core to compete with us … again that is great, competition makes the world go round!\
But you need to start from your own code not ours.
{% endhint %}

This article will help you get started, there isn't much to cover but what there is; is important to know!

## Dependency

System Core should only ever be installed via Package Manager!

### Why?

Dependency, multiple assets are dependent on it and they need a reliable way to detect when its installed and what version of it is installed. When System Core is imported into the assets folder as a package or copied in as lose code files there is no way for anyone to detect the version installed.

### Solution!

Package Manager, while its not great it is what Unity Technology has moved to and it does give us what we need in terms of a means to query and see what is installed and detect the version that is installed.

### How?

```csharp
using UnityEditor.PackageManager;
using UnityEditor.PackageManager.Requests;
```

These two namespaces give us everything we need to query what packages are installed and even kick off remove, update or installs operations.

{% hint style="info" %}
Package Manager processes are asynchronous so you will need a means to handle that. You can use background workers or other methods but we tend to prefer [Coroutines ](../../../company/asset-developers/editor-coroutines.md)as they are familiar to other Unity developers and also let us work with things that aren't thread safe.&#x20;

a

[Want to know how to use Editor Coroutines? read this article!](../../../company/asset-developers/editor-coroutines.md)
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
