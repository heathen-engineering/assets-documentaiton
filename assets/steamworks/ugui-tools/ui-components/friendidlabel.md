# FriendIdLabel

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

![](<../../../../.gitbook/assets/image (181).png>)

Similar to Friend ID Field but designed to work with a simple Text lable as opposed to an InputField.

Friend ID Label implaments [IUserProfile](../interfaces/iuserprofile.md) interface

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
