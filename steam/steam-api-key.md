---
description: How to find and use the Publisher Steam API Key
---

# 🔑 Steam API Key

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

If your planning on working with Steam Web API such as through PlayFab or really any other mechanism you will need to generate a "Publisher Steam API Key"

To do this first navigate to your Steam Developer Portal and select the Manage Groups option under the Users & Permissions menu

<figure><img src="../.gitbook/assets/image (13).png" alt="Manage user groups"><figcaption><p>The Users &#x26; Permissions panel</p></figcaption></figure>

From here you should create a new group which we will associate the key with, this is how we control what apps the key is associated with.

<figure><img src="../.gitbook/assets/image (1) (8).png" alt="Create a new group"><figcaption><p>Creating a new group</p></figcaption></figure>

Select the group and in the group page you will see an option on the right side of the screen to create a Web API Key

<figure><img src="../.gitbook/assets/image (20).png" alt="Create the Web API key"><figcaption><p>Creating the web API key</p></figcaption></figure>

Once created you view the key directly below that Edit Group menu and of course can revoke the key should it no longer be needed or be compromised. The "Manage Web API Key" option lets you white list specific IP addresses though this can be left blank and typically would be for uses like PlayFab.

<figure><img src="../.gitbook/assets/image (37).png" alt="Manage the API key"><figcaption><p>Managing the key</p></figcaption></figure>
