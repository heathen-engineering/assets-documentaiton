# Set User Name

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

A simple component meant to be attached to a UnityEngine.UI.RawImage

This can update the text with the indicated user's name and can optionally pull the local user's data on start up.

This will update as the linked user changes there name ... that is if the tracked user edits there name this will update accordingly.

## Definition

{% hint style="info" %}
This componenet has 2 variations one for each of Unity's text lables ... additonal variants will be added as Unity contentinues to add more UI frameworks.
{% endhint %}

```csharp
[RequireComponenet(typeof(TMPro.TextMeshProUGUI)]
public class TMProSetUserName : MonoBehaviour;
```

```csharp
[RequireComponent(typeof(UnityEngine.UI.Text))]
public class UGUISetUserName : MonoBehaviour
```

## Fields and Attributes

### useLocalUser

```csharp
public bool useLocalUser
```

{% hint style="warning" %}
This can only be set in the Unity Editor and will be false for run time created componenets or if not set.
{% endhint %}

This causes the componenet to grab the local user's ID on startup.

### ShowNickname

```csharp
public bool ShowNickname { get; set; }
```

Should the tool show the user's [nickname ](../../data-layer/user-data.md#nickname)if any or should it always show the Steam User Name.

### UserData

```csharp
public UserData UserData { get; set; }
```

This returns the UserData that this componenet is currently tracking. Setting this will cause this componenet to track the user you set to it and is the same as calling LoadAvatar;

## Methods

### Set Name

```csharp
public void SetName(UserData user);
```

```csharp
public void SetName(CSteamID user);
```

```csharp
public void SetName(ulong user);
```

Set the indicated user's name.
