# User Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

This scene demonstrates the use of [User Data ](../../data-layer/user-data.md)and displaying common information such as the user's avatar and name.

<figure><img src="../../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

This scene exists to draw your attention to the [User Data](../../data-layer/user-data.md) object. User Data is a struct Heathen has defined to wrap around the native [CSteamID ](../../../../company/steam/steamworks/csteamid.md)and the primitive ulong data types providing easy access to everything user related.

User Data can be used to read the name, nickname, level, status, friend ID, avatar image, rich presence data and much more about a friend. User Data is interchangeable with CSteamID and ulong and can be used anywhere those data types representing a Steam user are called for.

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../unity/components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

### [Friend Profile](../../unity/ugui-tools/prefabs/friend-profile.md)

Demonstrates the displaying of the local user's data. This prefab uses the[ Friend Profile](../../unity/ugui-tools/ui-components/friendprofile/) component script which its self uses [User Data](../../data-layer/user-data.md) to deliver the required information.

### [Friend Group](../../unity/ugui-tools/prefabs/friend-groups.md)

Demonstrates the display of the user's friend data in a manner similar to Steam's friend list.
