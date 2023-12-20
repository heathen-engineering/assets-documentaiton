---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# User Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This scene demonstrates the use of [User Data ](../data-layer/user-data.md)and displaying common information such as the user's avatar and name.

<figure><img src="../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

This scene exists to draw your attention to the [User Data](../data-layer/user-data.md) object. User Data is a struct Heathen has defined to wrap around the native [CSteamID ](../../../steam/csteamid.md)and the primitive ulong data types providing easy access to everything user related.

User Data can be used to read the name, nickname, level, status, friend ID, avatar image, rich presence data and much more about a friend. User Data is interchangeable with CSteamID and ulong and can be used anywhere those data types representing a Steam user are called for.

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

### [Friend Profile](../prefabs/friend-profile.md)

Demonstrates the displaying of the local user's data. This prefab uses the[ Friend Profile](../ui-components/friend-profile/) component script which its self uses [User Data](../data-layer/user-data.md) to deliver the required information.

### [Friend Group](../prefabs/friend-groups.md)

Demonstrates the display of the user's friend data in a manner similar to Steam's friend list.

{% hint style="info" %}
On your first run of a day you may notice that some friend avatar images or names do not load or load slowly. This is side effect of this use case and would not occur in a production environment.\
\
The cause is that Steam cashes this information on your local machine, when the information is first requested it can take time for that data to download. The sample scene doesn't wait and simply loads what information is available where typically you use the provided events or good design practices such as [bootstrapping ](../../../company/design/bootstrap-scene.md)and validation avoiding this issue.
{% endhint %}

## Testing

Assuming you are using an unmodified version of the sample scene and Steam Settings you will see messages appear in the Unity Editor Console log detailing each step of the initialization process.

<figure><img src="../../../.gitbook/assets/image (15) (1) (3).png" alt=""><figcaption><p>Example initialization messages</p></figcaption></figure>

In the event of an error details will be listed here along with troubleshooting guidance. In the event you require support please select the first error message in the log and press \[Ctrl + C] this will copy the full message and its stack trace to your clipboard. You can then paste that error into [Discord chat](https://discord.gg/eVVgM36) for live support or into a support email or similar.

Aside from the console output you will have a visual indication that Steam API is initialized correctly when your Steam User profile image, name, status and ID are displayed in the upper right corner of the screen.
