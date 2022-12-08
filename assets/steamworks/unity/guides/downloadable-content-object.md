---
description: Understanding Steam DLC and the Heathen Engineering tool kit
---

# Downloadable Content

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="warning" %}
#### Understanding Steam DLC

Its important to understand the proper usage of DLC. Most of this is a matter of configuration in the Steam Developer Portal. Please carefully and fully read the documentation for the feature. It can be found here [https://partner.steamgames.com/doc/store/application/dlc](https://partner.steamgames.com/doc/store/application/dlc)
{% endhint %}

![](<../../../../.gitbook/assets/image (183) (1) (1) (1) (1).png>)

The [Downloadable Content Object](../scriptable-objects/downloadable-content-object.md) helps you track the status of DLC. You can import the DLC you have defined in the Steam Developer Portal for this application by running the simulation such that Steam API is able to initialize and then clicking the Import button on the Steam Settings Downloadable Content list

![](<../../../../.gitbook/assets/image (157) (1) (1) (1).png>)

Once completed all of the DLC registered to your application will be listed under your Steam Settings

![](<../../../../.gitbook/assets/image (178) (1) (1) (1) (1).png>)

And can be used to test ownership of the indicated DLC. Please see the [Downloadable Content Object](../scriptable-objects/downloadable-content-object.md) for details on the use of the object.
