# Authentication Session

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public class AuthenticationSession
```

Used by the [Authentication ](../api/authentication.md)interface to represent an active authentication session

## Fields and Attributes

| Type                 | Name            | Comment                                                                                   |
| -------------------- | --------------- | ----------------------------------------------------------------------------------------- |
| bool                 | isClientSession | Is this a client or server session                                                        |
| CSteamID             | user            | The ID typically a user the session is related to                                         |
| CSteamID             | gameOwner       | The id of the owner of the game, if this is different than the user then this is barrowed |
| byte\[]              | data            | the ticekt data that was used to start the session                                        |
| EAuthSessionResponse | responce        | The responce recieved when validating a provided ticket                                   |
| bool                 | IsBarrowed      | The same as user == gameOwner                                                             |
| Action               | onStartCallback | the callback invoked when the session has started ... this is used internally             |

## Methods

### End

```csharp
public void End();
```

Ends this session&#x20;
