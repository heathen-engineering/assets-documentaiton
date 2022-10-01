# FriendIdField

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (168) (1) (1).png>)

The Friend ID Field control is meant to be used to display a User's Friend ID in a Read Only Input Field such that users can easily select it and copy and paste the result.

Friend ID can be used to add friends in your Steam Friends list so this method can be useful for user's to share there freind ID over Discord or other non-Steam platforms to incurage players to add them to friends.

For cases where both user's are current'y on Steam you can simply use the Friend API to send a Friend Invite.

Friend ID Field implaments [IUserProfile](../interfaces/iuserprofile.md) interface

## Inspector Fields

### Use Local User

If checked true the control will load the local user's image on start

## Fields

### UserData

```csharp
public UserData UserData { get; set; }
```

Gets or sets the UserData that this control is linked to

## Methods

### Apply

```csharp
public void Apply(UserData user)
```

Sets the UserData that this control is linked to.
