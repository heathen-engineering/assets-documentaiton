---
description: Installing the PhysKit asset from the Unity Asset Store
---

# Installation

## GitHub Sponsors

{% embed url="https://github.com/sponsors/heathen-engineering" %}

{% hint style="success" %}
Better for us and better for you!

Sponsoring Heathen on GitHub for $10 a month gets you access to the sorce repository for Steamworks, PhysKit and UX Complete.

\
See why GitHub sponsor is the hands down best way to Do More with Heathen in our [Licensing Article](../licensing/).
{% endhint %}

## New Installs

For new projects this couldn't be simplier.

Import into Unity as you normally would and it will install all dependencies for you.

## Updating Existing Installs

{% hint style="info" %}
When upgrading from PhysKit versions 2.16.0 or earlier you should fully remove your existing install before importing the new PhysKit package.



This will help insure a clean and efficent install process. This is due to System Core being moved out of Unity Asset Store and into GitHub as a dependency. The asset will handle this install process for you but needs any old versions removed first.
{% endhint %}

## Import

### GitHub Sponsors

If your a GitHub sponsor you have access to the source repository which you can install from directly in Unity via the Package Manager.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SourceRepo.git?path=/PhysKit/com.heathen.physkit
```

GitHub will prompt you to login if you haven't already, this is how it checks to make sure your a sponsor and have access to the repo. Once done it will install PhysKit and any required dependencies.

### Unity Asset Store

If you purchased through the Unity Asset Store simply import through Unity's normal method.

Once imported the asset will check for dependencies and if missing it will install them via the Package Manager.

## Prerequisites

Heathen's PhysKit asset will handle the install of all requirements for you. Our asset is also able to handle existing installs of its required componenets. You shouldn't need to do anything other than import our asset.

{% hint style="warning" %}
#### Legacy Code



If you have legacy, custom or otherwise not from the original source versions of System Core then Unity will cause merge conflcits when importing our asset.



You should not be using versions of System Core other than the version avialable from GitHub such as would be installed by the Package Manger as discribed below and as installed by our asset on import into a clean project.



The single most common installation issue is due to having a full or partial install of an old or customized version of System Core in your project when importing our asset. Our asset will not attempt to compile until System Core is properly installed. It accomplishes this by only compiling when the script define `HE_SYSCORE` is defined.



If you have questions or issues pealse reach out on our [Discord ](https://discord.gg/6X3xrRc)channel
{% endhint %}

## Import Process

When you import Heathen's Phys Kit it will test for the presence of System Core and if missing it will ask you if you want to install similar to the message shown below.

![](<../../.gitbook/assets/image (189) (1).png>)

When you click yes the system will use Package Manager to install System Core from GitHub.&#x20;

{% hint style="info" %}
Installing Unity Packages via Git URL as we do here requires that you have Git installed. as outlined in [Unity's documentation](https://docs.unity3d.com/Manual/upm-ui-giturl.html).\
\
If you don't have it already you can install Git from the following link:

* [https://git-scm.com/](https://git-scm.com)&#x20;

Note that this does NOT mean you will be using Git as a source repo, it is simply a set of protocols used by Package Manager to download the required code from its target repository.
{% endhint %}

{% hint style="warning" %}
If you get a message to the effect of \
`No git executable was found`\
\
This video might help you get it resolved

[https://youtu.be/F-8A8mJwL\_Y](https://youtu.be/F-8A8mJwL\_Y)



We are not associated with the creator we have simply been told that video has helped others with that error.



This thread might also be of help for you

[https://forum.unity.com/threads/no-git-executable-was-found-please-install-git-on-your-system-and-restart-unity.730511/](https://forum.unity.com/threads/no-git-executable-was-found-please-install-git-on-your-system-and-restart-unity.730511/)
{% endhint %}

When System Core is successfuly installed you will see messages in your console log similar to the following. These messages indicate what was installed, you can also review these in your Package Manager.

![](<../../.gitbook/assets/image (165) (1).png>)

{% hint style="info" %}
This always installs the latest code available and so the version number you see may very.
{% endhint %}

### I clicked no now what?

If for whatever reason you clicked no, or if you had an error and needed to install Git, or if you simply want to update System Core you can always use the `Help > Heathen > Phys Kit` menu entry to update any or all requriements.

&#x20;

![](<../../.gitbook/assets/image (180).png>)

## From Package Manager

If you dont like simply pressing buttons you can always install System Core from the package manager your self.

### Install System Core

This must be done from the Unity Package Manager to insure that the proper System Core assembly definition is installed and present in your project.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SystemCore.git?path=/com.heathen.systemcore
```
