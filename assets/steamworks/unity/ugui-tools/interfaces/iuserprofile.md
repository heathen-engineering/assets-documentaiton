# IUserProfile

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../../company/steam/">steam</a></td><td><a href="../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../physkit/">physkit</a></td><td><a href="../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../ux/">ux</a></td><td><a href="../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

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
