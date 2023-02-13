# User Data

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../">Guides and Tutorials</a></td><td><a href="../../../../../assets/steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../../assets/physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../../assets/physkit/">physkit</a></td><td><a href="../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../../assets/ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../../assets/ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../../assets/ux/">ux</a></td><td><a href="../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

The Heathen framework simplifies the concept of Steam User Data in our [UserData](../../../../../assets/steamworks/data-layer/user-data.md) object. This object is equitable and comparable to CSteamID and ulong meaning you can convert any CSteamID or ulong value to a UserData object.

```csharp
UserData user_fromUlong = 1234566;
UserData user_fromCSteamID = new CSteamID(1234566);
UserData user = UserData.Get(1234566);
```

This means you no longer need to "Get" a UserData object as you did in other steam integrations. The UserData object exposes all relevant information about the user in question with simple fields.&#x20;

{% hint style="info" %}
For full details see [UserData's documentaiton here](../../../../../assets/steamworks/data-layer/user-data.md).
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

There are a few pre-made components that can help display common UserData to the screen such as the [Set User Avatar](../../../../../assets/steamworks/unity/components/set-user-avatar.md) and [Set User Name](../../../../../assets/steamworks/unity/components/set-user-name.md) components. These simply set uGUI RawImage or uGUI Text or TMPro text fields.&#x20;

{% hint style="warning" %}
These are based on uGUI and sadly Unity has greatly fragmented its UI frameworks with 3 frameworks at current being supported and 1 of them having 2 variations that are "official".



We will maintain components like this as part of the framework but may need to move them to sample code in the future as Unity continues to fragment UI options. This isn't really a bad thing in that it gives you more options but does mean we cant assume the best or correct way to do a thing regarding UI and so may need to simply guide you on available options.



This issue has already seen the removal of Lobby List and other uGUI components for other areas of Steam API which have been moved to Sample Code. If you have questions or suggestions please let us know in our [Discord](https://discord.gg/6X3xrRc).
{% endhint %}
