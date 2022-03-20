---
description: Simply shows the user's image
---

# FriendAvatar

## Overview

![](<../../../../.gitbook/assets/image (188).png>)



Friend Avatar implaments [IUserProfile](../interfaces/iuserprofile.md) interface

## Inspector Fields

### Use Local User

If checked true the control will load the local user's image on start

### Evt Loaded

A simple Unity Event that is invoked when the image is loaded

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
