---
description: User eXperience asset from Heathen Engineering;
---

# Installation

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/steam/">Guides and Tutorials</a></td><td><a href="../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="learning/core-concepts/">User eXperience Tools</a></td><td><a href="learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="./">.</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

UX Complete and the extension package uGUI Extras are both standard Unity assets that do not require any special installation steps. Simply import the assets and your done.

### GitHub Sponsors

If your a GitHub sponsor you have access to the source repository which you can install from directly in Unity via the Package Manager.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SourceRepo.git?path=/UX/com.heathen.ux
```

GitHub will prompt you to login if you haven't already, this is how it checks to make sure your a sponsor and have access to the repo. Once done it will install UX and any required dependencies.

### Unity Asset Store

If you purchased through the Unity Asset Store simply import through Unity's normal method.

Once imported the asset will check for dependencies and if missing it will install them via the Package Manager.

## New Input System

{% hint style="info" %}
UX and all related assets DO work with both the old and new input systems.
{% endhint %}

{% hint style="warning" %}
In recent updates Unity has changed the process for enabling the "New" input system such that toggling the Player Settings to use the "New" input system does **NOT** install the input system package.



You must install the Input Package system from the Package Manager your self to get it to work. Our asset is coded to use either the new or the old depending on which is installed. If you set the Project Settings to use the "New" input system without installing it from the Package Manager then you will get compiler errors.&#x20;
{% endhint %}

![](<../../.gitbook/assets/image (179) (1) (1).png>)

## Troubleshooting

Having issues with Package Manager install or Git install?

Read our [Pacakge Manager Install](../../company/fundamentals/package-manager-installs/) article to get it fixed
