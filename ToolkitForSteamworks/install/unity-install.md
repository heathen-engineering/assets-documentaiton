# Unity Install

## How to Install

<details>

<summary>GitHub Sponsor | Patreon</summary>

We strongly recommend you clone the repository to your local disk. The simplest way to do this is to use [GitHub Desktop](https://desktop.github.com/). Once you have that installed, you can easily clone any repository to your local disk.

<figure><img src="../.gitbook/assets/image (228).png" alt=""><figcaption></figcaption></figure>

Once you have the repository cloned to your local disk you can use Unity's Package Manager to import any of the packages you like into your project.

<figure><img src="../.gitbook/assets/image (229).png" alt=""><figcaption></figcaption></figure>

1. Open the Unity Package Manager
2. Click the + button
3. Select the "Add from Disk" option
4. Select the package.json for the asset you would like to import

You can follow the instructions in the Git Repo to guide you to each package. Here is a screenshot of the document ... give it a read.

<figure><img src="../.gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Unity Asset Store</summary>

Install the package from Unity Asset Store as you would any other package.&#x20;

</details>

### How to Install Samples

No matter where you licensed and installed the package from installing the samples is the same.

1. Open the Unity Package Manager
2. <mark style="color:$warning;background-color:$warning;">\[Important]</mark> Click the "**In Project**" tab
3. Find the "Packages - Heathen Group" grouping
4. Select "Toolkit for Steamworks SDK"
5. Select the "Samples" tab.

<figure><img src="../.gitbook/assets/image (384).png" alt=""><figcaption></figcaption></figure>

## Install Steamworks.NET

{% hint style="danger" %}
DO NOT install Steamworks.NET from the Releases folder in its repo
{% endhint %}

{% hint style="danger" %}
DO NOT copy Steamworks.NET into your Assets folder ... that is not installing.
{% endhint %}

{% hint style="success" %}
DO Clone the Steamworks.NET repository to your local disk and the Package Manager - Add from Disk method.

or

Allow the Toolkit for Steamworks SDK to install it for you.
{% endhint %}

## Troubleshooting

### EntryPointNotFoundException

This or similar exceptions referring to SteamInternal\_SteamAPI\_Init assembly or similar references to Steam's assemblies.&#x20;

#### Cause

You have a copy of Steam's assemblies in your Asset folder, or you did and haven't restarted since. This means that Unity is using the wrong assembly. You should NEVER have Steamworks.NET or any of its assemblies in your Asset folder.

#### Fix

Remove the offending assemblies usually found in the Plugins folder or similar. You may need to reinstall Steamworks.NET to repair any bad merges that resulted from the duplicate assembly.

### Not Found in Namespace

So you installed, and now XXXX is not found in the X namespace.

#### Cause

Something is messing with your assembly references. The usual culprits:\
You had Toolkit for Steamworks Foundation installed, then installed the full version on top of that. This will have caused Unity to merge the assembly defines, breaking references.

#### Fix

Make sure you remove Foundation first. Once it's gone, you need to repair your current install. If you used the Add from Disk option to install the package from GitHub, open up GitHub Desktop and revert the changes, you should find that 1 or more assembly defs or rather their meta files, had changes. If you installed from Unity Asset Store, try simply reimporting
