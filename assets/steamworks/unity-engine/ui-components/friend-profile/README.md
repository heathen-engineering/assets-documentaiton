# Friend Profile

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

Friend profile is a simple implementation of the [IUserProfile ](../../programming-tools/iuserprofile.md)interface and is used in the prefab examples for [FriendList ](../friend-list.md)and other controls. In most cases you will want to create your own "Friend Profile" UI script and can use the included FriendProfile as an example to get started with.

## Creating your own

```csharp
public class MyFriendProfileScript : MonoBehaviour, IUserProfile
{
    //...
}
```

You can implement the [IUserProfile](../../programming-tools/iuserprofile.md) interface on your custom profile script and this will allow all of the other profile related UI tools to work with it. That is you can create a custom profile like this and the [FriendList](../friend-list.md), [FriendGroup ](../friend-group.md)and other friend related controls will be able to work with it thanks to the [IUserProfile](../../programming-tools/iuserprofile.md) interface.

The [IUserProfile](../../programming-tools/iuserprofile.md) interface requires you to implement two features

```csharp
private UserData _userData;
public UserData UserData
{
    get => _userData;
    set => Apply(value);
}

public void Apply(UserData user)
{
    _userData = user;
    //Update your UI for the new user
}
```

The [UserData ](../../../data-layer/user-data.md)field and the Apply method are the two required features of the [IUserProfile](../../programming-tools/iuserprofile.md) interface. You can use the implementation shown above as a good starting off point adding whatever code your UI requires to the Apply method.

## Events

The following event is available on the FriendProfile that ships with the kit.

{% hint style="info" %}
This object is meant as an example to get you started with creating your own.
{% endhint %}

### evtLoaded

```csharp
public UnityEvent evtLoaded;
```

A simple event that is raised when the [UserData ](../../../data-layer/user-data.md)is loaded to the UI controls. This event has no arguments.

## Fields and Attributes

The following describes the definition of the FriendProfile that ships with the kit.

{% hint style="info" %}
This object is meant as an example to get you started with creating your own.
{% endhint %}

### useLocalUser

```csharp
private bool useLocalUser;
```

A private field only accessible in the Unity Inspector, you can set this to true and the profile will automatically load the local user's [UserData ](../../../data-layer/user-data.md)on start.

### appendNickname

```csharp
public bool appendNickname;
```

If false then the display name field will get the Nickname if available and Friend name if not. If true then the display name will always be the Friend name and the nickname field will be used for nick if available.

### messageOptions

```csharp
public MessageOptions messageOptions;
```

Defines the options for displaying status messages for the profile in question such as online, offline, if they are in a game or other game and rather or not the other game should be named. This uses the [MessageOptions ](message-options.md)sub struct.

### avatar

```csharp
private RawImage avatar;
```

A private field pointing to the RawImage control that will be used to display the user's avatar. This can only be set in the Unity Inspector.

### displayName

```csharp
private TextField displayName;
```

The settings and options for displaying the user's name, this uses the [TextField ](text-field.md)sub struct.

### nickName

```csharp
private TextField nickName;
```

The settings and options for displaying the user's nick name, this uses the [TextField ](text-field.md)sub struct.

### statusLabel

```csharp
private TextField statusLabel;
```

The settings and options for displaying the user's status as text, this uses the [TextField ](text-field.md)sub struct.

### statusImage

```csharp
private ImageField statusImage;
```

The settings and options for displaying the user's status as an image, this uses the [ImageField](image-field.md) sub struct.

### friendId

```csharp
private TextField friendId;
```

The settings and options for displaying the user's friend ID, this uses the [TextField ](text-field.md)sub struct.

### level

```csharp
private TextField level;
```

The settings and options for displaying the user's status as text, this uses the [TextField ](text-field.md)sub struct.

### panel

```csharp
private ImageField statusImage;
```

The settings and options for displaying the user's status as a change in panel, this uses the [ImageField](image-field.md) sub struct.
