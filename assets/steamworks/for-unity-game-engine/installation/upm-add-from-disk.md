---
description: Unity Package Manager Add from Git URL
---

# UPM Add from Disk

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Requirements

Using the Unity Package Manager to Add a package from Disk is very much similar to the Add from Git URL method but reads the data from disk as opposed to the web. As this does read from your local disk your first step is to clone all the repos you require down to your local disk ... to do so follow these steps.

### GitHub Desktop

This is a tool from GitHub that makes it easy to "clone" (copy to disk) repositories off of GitHub's website.

{% embed url="https://desktop.github.com/" %}

Get that installed and restart your PC then move on to the next step

### Clone Repositories

This is "Git"s little word for make a local workspace, it literally 1 button press ... maybe 2.

Here is how you do it ... then we will show you which repos you need to go clone.

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### Step 1

Click the big green button that says `<> Code`&#x20;

#### Step 2

Click `Open with GitHub Desktop`

...

Done!

Now that we have the hard part out of the way here are the repos you will need&#x20;

### Steamworks.NET

{% embed url="https://github.com/rlabrecque/Steamworks.NET" %}

### System Core

{% embed url="https://github.com/heathen-engineering/SystemCore" %}

### Free Foundation

{% hint style="info" %}
If your looking to install the Foundation version also open it
{% endhint %}

{% embed url="https://github.com/heathen-engineering/SteamworksFoundation" %}

### GitHub Sponsors

{% hint style="info" %}
If your a GitHub Sponsor and looking to do this with Steamworks Complete ... open the Source Repo
{% endhint %}

{% embed url="https://github.com/heathen-engineering/SourceRepo" %}

## Add from Disk

If your a GitHub sponsor you have access to the source repository which you can install from directly in Unity via the Package Manager.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from disk..." option\
   ![](<../../../../.gitbook/assets/image (1).png>)
4. Select the desired folder.

As to knowing which folder is the "desired" folder ... its always the folder that contains the `package.json` file in it. Follows are the current names of those folders for each requirement as follows

#### Steamworks.NET

`com.rlabrecque.steamworks.net`

#### System Core

`com.heathen.systemcore`

For the asset packages its&#x20;

#### Steamworks Foundation

`com.heathen.steamworksfoundation`

#### Steamworks Complete

`com.heathen.steamworkscomplete`

``
