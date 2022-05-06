---
description: Installing Wood Props from Heathen's Breakable collection
---

# Installation

## GitHub Sponsors

{% embed url="https://github.com/sponsors/heathen-engineering" %}

{% hint style="success" %}
Better for us and better for you!

Sponsoring Heathen on GitHub for $10 a month gets you access to the source repository for Steamworks, PhysKit and UX Complete; as well as our growing library of art assets.

\
See why GitHub sponsor is the hands down best way to Do More with Heathen in our [Licensing Article](../../../licensing/).
{% endhint %}

### Import

Import the PhysKit Complete asset first, this is a dependency and provides the logic for breaking the assets and the assets are stored as a "sample" of it.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SourceRepo.git?path=/PhysKit/com.heathen.physkit
```

GitHub will prompt you to login if you haven't already, this is how it checks to make sure your a sponsor and have access to the repo. Once done it will install PhysKit and any required dependencies.

### Samples

Breakable Wood Props is exposed in the Package Manager under the samples for PhysKit Complete. This is because the breakable feature used in the prefabs is part of PhysKit Complete.

To install it simply install PhysKit Complete from Package Manager as described in its installation page, then expand the Samples drop down and import the "Breakable Wood Props".

{% hint style="success" %}
This will import the props and the configured prefabs which will be using the default Unity material.



We do this so that the kit is compatible with all rendering pipelines, you can download and install the materials you like from the following links.
{% endhint %}

### Materials

The models and prefabs will be imported into your project using the Unity Default Material (white/grey mat); The following links can be used to download free materials as seen in the promotional images.

{% embed url="https://assetstore.unity.com/packages/2d/textures-materials/wood-props-materials-standard-built-in-220518" %}

{% embed url="https://assetstore.unity.com/packages/2d/textures-materials/wood-props-materials-standard-urp-220650" %}

{% embed url="https://assetstore.unity.com/packages/2d/textures-materials/wood-props-materials-standard-hdrp-218315" %}
