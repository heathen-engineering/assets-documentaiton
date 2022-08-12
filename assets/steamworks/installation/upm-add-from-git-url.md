---
description: Unity Package Manager Add from Git URL
---

# UPM Add from Git URL

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

### Free Foundation

Steamworks Foundation is a freely available "lite" version of Heathen's Steamworks system. It is available on GitHub as is, without warranty. It is licensed under the MIT license agreement with a Common Clause condition allowing you to use it for any purpose ... other than releasing a competing Steamworks Integration :sunglasses:

To install Steamworks Foundation&#x20;

This must be done from the Unity Package Manager to insure that the proper Steamworks Foundation assembly definition is installed and present in your project.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SteamworksFoundation.git?path=/com.heathen.steamworksfoundation
```

### GitHub Sponsors

{% hint style="info" %}
You must be an active GitHub Sponsor at the $10 level or higher for this to work. You must also be logged into the same GitHub user that sponsored. See our [Package Manager article](../../../company/concepts/fundamentals/package-manager-installs.md#im-a-sponsor-but-cant-install) for troubleshooting tips.
{% endhint %}

If your a GitHub sponsor you have access to the source repository which you can install from directly in Unity via the Package Manager.

1. Open the Package Manager
2. Click the "+" (plus) button located in the upper left of the window
3. Select the "Add package from git URL..." option\
   <img src="../../../.gitbook/assets/image (144).png" alt="" data-size="original">
4. Enter the URL below and press add.

```
https://github.com/heathen-engineering/SourceRepo.git?path=/Steamworks/com.heathen.steamworkscomplete
```

GitHub will prompt you to login if you haven't already, this is how it checks to make sure your a sponsor and have access to the repo. Once done it will install Steamworks and any required dependencies.

