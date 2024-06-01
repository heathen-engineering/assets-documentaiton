---
description: So you have a problem
cover: ../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Troubleshooting

{% hint style="success" %}
#### Like what you are seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This section will cover the most common installation issues and how to resolve them. Before we get into the common issues and causes here are a few key bits of information.

## Unity Merge

You may know that Unity attempts to merge assets on import.&#x20;

### **So what does that mean?**

Every asset in your Unity project has a GUID associated with it, which is a globally unique ID so Unity can know that folder A is the same folder A no matter where you move it or even rename it.

### **Why is this relevant?**

If you have any old or customized versions of System Core, Steamworks.NET, etc. then Unity will attempt to merge the new stuff you are installing with the old, even if you are doing it from Package Manager. This will break a lot of things and make a huge mess.

### **How to prevent the issue?**

First fully remove any non-package manager installed versions of Steamworks.NET, System Core or any old Heathen assets ... old Heathen assets would have a copy of System Core in them so remove that.

### **How to fix it when it goes bad?**

So let us say you tried to install, forgot to clean out an old Steamworks.NET or missed a few files or something. To clean this you first should remove the Package Manager version using Package Manager. Next clean out the old offending files and finally reinstall from Package Manager.

So if you have compilation errors or if your Script Defines are a bit of a mess you might need to install these manually from Package Manager ... you can find the process for that [here](troubleshooting.md#from-package-manager).

## Script Defines

Script definitions are used by Unity, Steamworks.NET and Heathen to know what is installed and ready to use and what platform it is currently set to. These definitions are used in code to enable or disable code from compiling under various conditions. This means even with the script files present some code just won't be seen by the compiler unless these definitions are set up properly.

Heathen no longer uses global script definitions but references all definitions as part of the assembly definitions.

![Note the "Version Defines" at the bottom of the inspector window](<../../../.gitbook/assets/image (171).png>)

These definitions exist only if the related assembly is present. If these defines are not present the code will not compile.

### STEAMWORKSNET

This is the script defined set by Steamworks.NET

It indicates that Steamworks.NET is present but does not indicate that it should be complied with. That is the presence of the define `DISABLESTEAMWORKS` will still be respected and prevent any compilation of Steamworks-dependent code.

### HE\_SYSCORE

This is the script defined set by System Core

It indicates that System Core is present, System Core is a framework that all Heathen assets are dependent on and must be present for any of the code to compile.

## No git executable was found

{% hint style="info" %}
Or any other Unity Package Manager-related issue
{% endhint %}

{% embed url="https://kb.heathenengineering.com/company/concepts/package-manager-install" %}

## How to install from disk

So if you can't or won't install Git command so that Unity's Package Manager can read Git repositories directly ... then be prepared to have a hard time with most community and open source assets but we can help you install Heathen's assets without it.

{% hint style="info" %}
Installing Git doesn't mean you have to use Git in your project as source control. It is simply a command line tool that allows Unity's Package Manager to read packages directly from their Git Repos on the web.
{% endhint %}

1st thing you need to do is clone the repository to your local disk (NOT YOUR PROJECT):

{% hint style="danger" %}
DO NOT simply copy the repo into your Unity project\
That will NOT work, it will break references it is not the correct solution.
{% endhint %}

Once you have cloned the repo to your disk ... which by the way is easier to do if you have Git installed ... but you can do it by downloading a zip and extracting it.

Once you have the repository local on your disk you use the Unity Package Manager's "Install from Disk" option to install whatever it is for example System Core, Steamworks.NET, etc.

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

This will open a file browser window, you should navigate to the folder that contains the package.json file in the repo for example if you were manually doing Steamworks Complete it would look like\
`./SourceRepo/Unity/Steamworks/com.heathen.steamworkscomplete/package.json`

Click okay and now the Unity Package Manager will install that package properly.

### Why you shouldn't use zips

the main issue with downloading a zip and using it is version control and update. Even if you insist on installing from a local disk you should still do so via Git Desktop or a similar Git install.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Unlike a zip this will be a version-managed repository so updating is a single button click, it will also show you change history and compare files on the local disk with the repo making it easy to understand what changed, when and by whom.

Using a zip is not the easiest method, it is highly error-prone, slower to download, and unable to directly update. Downloading Git Desktop or similar doesn't mean you have to use Git in your projects, it doesn't mean you are bound to Git Hub or anything it is simply a free tool with a superior in every solution to this problem

## XXXX did not install

So for example System Core did not install or Steamworks.NET did not install

When you install a Heathen asset you should get a dialog box to pop up and let you know if it sees something missing and ask you if you want to install it. If you click install it will then try and install it from Package Manager.

**But what if you never see the dialogue?**

Well, that means 1 of 2 things is true.

Either you already have it installed or had it installed so its Script Defines are still present

or

You have compiler errors in your project preventing our editor script from running.

If it's that you have script defines in place for code you don't have installed simply remove the defines.

If it's that you have compiler errors and so our scripts are not running, simply install the requirements directly ... you can find instructions on how in [this section](broken-reference).

## XXXX is not found

So for example SteamSettings is not found in namespace XXXX or otherwise some message indicating that something you know is installed is not visible in the code.

This can be due to missing script definitions, you being on the wrong build target or you using an assembly definition that is not referencing the required assemblies.

#### Missing Script Defines

So if you have installed System Core, Steamworks.NET, etc. and the related script defined as noted above is not present. This can happen if you have compiler errors preventing the editor scripts from adding it. The simple fix is to simply add those definitions manually.

#### Build Target

Steamworks.NET will only compile for Windows, Mac and Linux client and server builds. If you have it set to anything else it will not compile and anything dependent on it will thus break. So if you are creating a code base that is multi-platform it is up to you to wrap your dependent code in platform checks e.g.

```csharp
#if DISABLESTEAMWORKS
    //Steam is not present
#else
    //Steam is present
#endif
```

#### Assembly Definitions

{% embed url="https://docs.unity3d.com/Manual/ScriptCompilationAssemblyDefinitionFiles.html" %}

This is a way to split a code base up into assemblies for faster and simpler compilation. Most Unity assets do this, all Unity Package Manager assets do this. If you are trying to use System Core, Steamworks.NET or Heathen's Steamworks Foundation or Complete in anything that has an assembly definition you will need to reference the related assembly definitions

You can view and edit the references a given assembly define as other defines in the Unity Inspector for your Assembly Definition.

![](<../../../.gitbook/assets/image (165).png>)

## Missing namespace

If you have errors coming from Heathen's code to the effect of&#x20;

![Or similar](<../../../.gitbook/assets/image (122).png>)

Then the problem is you either removed Steamworks.NET from the Package Manager or more likely your target platform is not valid. Steamworks.NET will only compile for PC, Mac or Linux ... not Windows Universal or any other platform.
