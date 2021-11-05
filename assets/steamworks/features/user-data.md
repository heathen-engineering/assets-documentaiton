---
description: >-
  User Data stores information about Steam users including the name, icon /
  avatar and persona state information.
---

# User Data

This object is used to manage a user's Steam data, such as the user's avatar, display name and state information e.g. Online, Offline, etc. The only UserData object created at development time is the "Local User Data" object, and this is created automatically for you. All other User Data objects are either created automatically for you when your user encounters a new Steam User such as members of a Steam Lobby, or when you request User Information from the system.

{% hint style="info" %}
A "Local User Data" object is created for you when you create the Steam Settings object. This object will store the local user's data as populated on Steam Initialization. As far as the use of each artifact type they are summarized below.
{% endhint %}

## Examples

### Get local user data

The local user is a special case; the system loads the local user's data on initialization and stores it in the "Local User Data" which is accessible from the Steam Settings object. You can get this object via code through the `user` member of the `client` object.

```csharp
var userData = SteamSettings.Client.user;
```

You can also reference this object at dev time by creating a reference on your script of type `UserData` and then dragging the reference from your Steam Settings object.

```csharp
public UserData localUser;
```

![Image of the example Steam Settings that come with the package](<../../../.gitbook/assets/image (17).png>)

### Get a UserData object by user id

You can use the `SteamSettings` object to fetch a `UserData` object for any user you have the id for. The `userId` can be of type `CSteamId` or `ulong` both types are handled.

```csharp
var user = SteamSettings.Client.GetUserData(userId);
```

### Get a user's icon / avatar

The icon or avatar of a user is located in the `avatar` member on the `UserData` object. Its of type `Texture2D` and can be accessed such as:

```csharp
image.texture = userData.avatar;
```

### Get a user's name

The name of a user is located in the `DisplayName` member on the `UserData` object. Its of type `string` and can be accessed such as:

```csharp
string userName = user.DisplayName;
```
