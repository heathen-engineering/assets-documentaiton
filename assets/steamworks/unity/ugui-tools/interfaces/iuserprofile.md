# IUserProfile

<figure><img src="../../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

A simple interface which can be applied to any visual representation of a User such as avatar images, names or even complex UI elements that display many aspects of user data. Several examples of this interface are present in the uGUI Tools package.

Examples:

* FriendAvatar
* FriendIdLable
* FriendName
* FriendProfile

## Fields

### UserData

```csharp
UserData UserData { get; set; }
```

Provides a standard approch to reading and setting the UserData object applied to this object. Typically the set portion of this field would simply call the Apply method.

## Methods

### Apply

```csharp
void Apply(UserData user);
```

A method which can be used to apply a given UserData object.
