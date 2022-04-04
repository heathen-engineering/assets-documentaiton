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

System Core should only ever be installed via Package Manager! You can check rather System Core is installed and what version is installed using the Package Manager namespace in Unity.

[To learn more, read this article.](../../../company/asset-developers/package-manger-in-c.md)

## Conditional Compile

System Core creates a script define `HE_SYSCORE` when it is installed properly. You can use this script define to drive conditional compilation for example.

```csharp
#if HE_SYSCORE
    //System Core is installed and available
#else
    //System Core is not installed, maybe you should ask them to install it?
#endif
```
