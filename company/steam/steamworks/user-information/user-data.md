# User Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The Heathen framework simplifies the concept of Steam User Data in our [UserData](../../../../assets/steamworks/unity-engine/data-layer/user-data.md) object. This object is equitable and comparable to CSteamID and ulong meaning you can convert any CSteamID or ulong value to a UserData object.

```csharp
UserData user_fromUlong = 1234566;
UserData user_fromCSteamID = new CSteamID(1234566);
UserData user = UserData.Get(1234566);
```

This means you no longer need to "Get" a UserData object as you did in other steam integrations. The UserData object exposes all relevant information about the user in question with simple fields.&#x20;

{% hint style="info" %}
For full details see [UserData's documentaiton here](../../../../assets/steamworks/unity-engine/data-layer/user-data.md).
{% endhint %}

## Use Cases

### Local User

The most common use case is to fetch the local user's information. This can be done with a single line call.

```csharp
using HeathenEngineering.SteamworksIntegration.API;

// ...

var localUser = User.Client.Id;
```

For example if you wanted to get the local user's name as it appears on Steam.

```csharp
using HeathenEngineering.SteamworksIntegration.API;

// ...

var userName = User.Client.Id.Name;
```

### Avatar Image

Unlike previous iterations we only load the image when requested, this save memory usage by only loading avatars that are requested.

```csharp
using HeathenEngineering.SteamworksIntegration.API;

// ...

if(User.Client.Id.Avatar != null)
{    
    // The avatar is already loaded
}
else
{
    User.Client.Id.LoadAvatar((result) => 
    {
        //Result will be the avatar if we could load it else null
    });
}
```

Note the Avatar field checks for loaded avatar images and returns the matching image if found.

The LoadAvatar method does similar but asynchronously and will load the image if not found. It does this by taking an Action as a parameter and invoking it when the image is found or loaded as required.

If your not aware of what a callback is see this [article](../../../development/lambda-expressions.md#callbacks).

### Display User information

There are a few pre-made components that can help display common UserData to the screen such as the [Set User Avatar](../../../../assets/steamworks/unity/components/set-user-avatar.md) and [Set User Name](../../../../assets/steamworks/unity/components/set-user-name.md) components. These simply set uGUI RawImage or uGUI Text or TMPro text fields.&#x20;

{% hint style="warning" %}
These are based on uGUI and sadly Unity has greatly fragmented its UI frameworks with 3 frameworks at current being supported and 1 of them having 2 variations that are "official".



We will maintain components like this as part of the framework but may need to move them to sample code in the future as Unity continues to fragment UI options. This isn't really a bad thing in that it gives you more options but does mean we cant assume the best or correct way to do a thing regarding UI and so may need to simply guide you on available options.



This issue has already seen the removal of Lobby List and other uGUI components for other areas of Steam API which have been moved to Sample Code. If you have questions or suggestions please let us know in our [Discord](https://discord.gg/6X3xrRc).
{% endhint %}
