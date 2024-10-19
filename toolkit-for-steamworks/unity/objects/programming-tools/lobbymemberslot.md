---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# LobbyMemberSlot

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

An abstract class used by the [Party Lobby Control](../ui-components/party-lobby-control.md) to represent a user slot in the UI.

```csharp
using HeathenEngieering.SteamworksIntegration.UI;
```

```csharp
public abstract class FriendInviteButton;
```

## Events

### InviteUserRequest

A UnityEvent to be invoked when the player has indicated that they would like to invite a user to join the indicated lobby. This allows the slot to act like a button that when pressed will start the process of selecting and inviting a user to join the lobby.

```csharp
public UnityEvent InviteUserRequest;
```

### RemoveUserRequest

A UnityEvent to be invoked when the player has indicated that they would like to ask the user that is represented by this slot to leave the lobby.

```csharp
public UnityEvent RemoveUserRequest;
```

## Fields and Attributes

### Interactable

Controls rather the control is interactable or not

```csharp
public abstract bool Interactable { get; set; }
```

## Methods

### SetUser

Set the user this slot represents if any

```csharp
public abstract void SetUser(LobbyMemberData user)
```

### GetUser

Get the user that is set to this slot if any

```csharp
public abstract LobbyMemberData GetUser()
```

### ClearUser

Clear the user from this slot

```csharp
public abstract void ClearUser()
```
