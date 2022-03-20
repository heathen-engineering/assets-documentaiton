# FriendIdLabel

## Overview

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
