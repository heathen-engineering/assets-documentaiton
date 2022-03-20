# IUserProfile

## Overview

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
