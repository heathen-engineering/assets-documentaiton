---
description: So you have a problem
---

# Troubleshooting

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

This section will cover the most common installation issues and how to resolve them. Before we get into the common issues and causes here are a few key bits of information.

## Unity Merge

You may know that Unity attempts to merge assets on import.&#x20;

### **So what does that mean?**

Every asset in your Unity project has a GUID associated with it, that is a globally unique ID so Unity can know that folder A is the same folder A no matter where you move it or even rename it.

### **Why is this relevant?**

If you have any old or customized versions of System Core, Steamworks.NET, etc. then Unity will attempt to merge the new stuff your installing with the old, even if your doing it from Package Manager. This will break a lot of things and make a huge mess.

### **How to prevent the issue?**

First fully remove any non-package manager installed versions of Steamworks.NET, System Core or any old Heathen assets ... old Heathen assets would have a copy of System Core in them so remove that.

### **How to fix when it goes bad?**

So lets say you tried to install, forgot to clean out an old Steamworks.NET or missed a few files or something. To clean this you first should remove the Package Manager version using Package Manager. Next clean out the old offending files and finally reinstall from Package Manager.

So if you have compilation errors or if your Script Defines are a bit of a mess you might need to install these manually from Package Manager ... you can find the process for that [here](troubleshooting.md#from-package-manager).

## Script Defines

Script defines are used by Unity, Steamworks.NET and Heathen to know what is installed and ready to use and what platform its current set to. These defines are used in code to enable or disable code from compiling under various conditions. This means even with the script files present some code just wont be seen by the compiler unless these defines are set up properly.

Heathen no longer uses global script defines but references all defines as part of the assembly definitions.

![Note the "Version Defines" at the bottom of the inspector window](<../../../../.gitbook/assets/image (171).png>)

These defines exist only if the related assembly is present. If these defines are not present the code will not compile.

### STEAMWORKSNET

This is the script define set by Steamworks.NET

It indicates that Steamworks.NET is present but does not indicate that it should be complied. That is the presence of the define `DISABLESTEAMWORKS` will still be respected and prevent any compilation of Steamworks dependent code.

### HE\_SYSCORE

This is the script define set by System Core

It indicates that System Core is present, System Core is a framework that all Heathen assets are dependent on and must be present for any of the code to compile.

## No git executable was found

{% hint style="info" %}
Or any other Unity Package Manager related issue
{% endhint %}

{% embed url="https://kb.heathenengineering.com/company/concepts/package-manager-install" %}

## XXXX did not install

So for example System Core did not install or Steamworks.NET did not install

When you install a Heathen asset you should get a dialog box to pop up and let you know if it sees something missing and ask you if you want to install it. If you click install it will then try and install it from Package Manager.

**But what if you never see the dialog?**

Well that means 1 of 2 things is true.

Either you already have it installed or had it installed so its Script Defines are still present

or

You have compiler errors in your project preventing our editor script from running.

If its that you have script defines in place for code you don't have installed simply remove the defines.

If its that you have compiler errors and so our scripts are not running, simply install the requirements directly ... you can find instruction on how in [this section](broken-reference).

## XXXX is not found

So for example SteamSettings is not found in namespace XXXX or otherwise some message indicating that something you know is installed is not visible in code.

This can be due to missing script defines, or you being on the wrong build target or you using an assembly definition that is not referencing the required assemblies.

#### Missing Script Defines

So if you have installed System Core, or Steamworks.NET, etc. and the related script define as noted above is not present. This can happen if you have compiler errors preventing the editor scripts from adding it. The simple fix is to simply add those defines manually.

#### Build Target

Steamworks.NET will only compile for Windows, Mac and Linux client and server builds. If you have it set to anything else it will not compile and anything dependent on it will thus break. So if your creating a code base that is multi-platform it is up to you to wrap your dependent code in platform checks e.g.

```csharp
#if DISABLESTEAMWORKS
    //Steam is not present
#else
    //Steam is present
#endif
```

#### Assembly Definitions

{% embed url="https://docs.unity3d.com/Manual/ScriptCompilationAssemblyDefinitionFiles.html" %}

This is a way to split a code base up into assemblies for faster and simpler compilation. Most Unity assets do this, all Unity Package Manager assets do this. If your trying to use System Core, Steamworks.NET or Heathen's Steamworks Foundation or Complete in anything that has an assembly definition you will need to reference the related assembly definitions

You can view and edit the references a given assembly define has toward other defines in the Unity Inspector for your Assembly Definition.

![](<../../../../.gitbook/assets/image (165).png>)

## Missing namespace

If you have errors coming from Heathen's code to the effect of&#x20;

![Or similar](<../../../../.gitbook/assets/image (122).png>)

Then the problem is you either removed Steamworks.NET from the Package Manager or more likely your target platform is not valid. Steamworks.NET will only compile for PC, Mac or Linux ... not Windows Universal or any other platform.
