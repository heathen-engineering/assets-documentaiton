# FriendIdField

## Overview

![](<../../../../.gitbook/assets/image (168).png>)

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
