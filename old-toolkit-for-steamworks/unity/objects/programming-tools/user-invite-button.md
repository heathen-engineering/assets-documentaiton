---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# User Invite Button

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

An abstract class used by the [Friend Invite Dropdown](../ui-components/friend-invite-dropdown.md) to display the list of friends and handle click events driving the invite process.

```csharp
using HeathenEngieering.SteamworksIntegration.UI;
```

```csharp
public abstract class UserInviteButton;
```

## Events

### Click

A UnityEvent that should be invoked when the UI element is clicked and should report the user that is related to the click e.g. if a user clicks on a button representing Friend A then the event should report Friend A.

```csharp
public UnityUserAndPointerDataEvent Click;
```

The typical handler for this event would take the form of

```csharp
public void Handler(UserAndPointerData data)
{
    //Do Work
}
```

## Fields and Attributes

### UserData

Represents the user this button is related to

```csharp
public UserData UserData { get; protected set; }
```

This can only be set by the inheriting class and is the [UserData](../classes/user-data.md) of the user this button represents.

## Methods

### OnPointerClick

This is an implementation of the `UnityEvent.EventSystem.IPointerClickHandler` and will be invoked when the user clicks on the UI element. This method will in turn invoke the [Click ](user-invite-button.md#click)event for you.

```csharp
public void OnPointerClick(PointerEventData eventData)
```

### SetFriend

This should be implamented by the inheriting class and should be used to configure the UI display to display the required features of the indicated user. You see an example of this in the `BasicFriendInviteButton` provided in the asset.

```csharp
public abstract void SetFriend(UserData user);
```

The BasicFriendInviteButton component included with the asset implaments this method such as

```csharp
public override void SetFriend(UserData user)
{
    this.UserData = user;
    avatar.UserData = user;
    displayName.UserData = user;
    status.UserData = user;
}
```
