# FriendList

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../../company/steam/">steam</a></td><td><a href="../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../physkit/">physkit</a></td><td><a href="../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../ux/">ux</a></td><td><a href="../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

![](<../../../../../.gitbook/assets/image (174).png>)

A simple linear list of friends, you can specify via the filter value what types of friends this list should populate. This will update its list when there is an update to persona data detected by Steam client. This means most state changes for a player's friends and followed users will be automatically detected and updated adjusting the list as required.

## Inspector Fields

### Filter

Describes the types of friends that should be included in this list options include

* All\
  Simply lists all friends
* InThisGame\
  Lists friends that are playing this game
* InOtherGame\
  Lists friends that are playing a game but not this one
* InAnyGame\
  Lists friends that are playing any sort of game
* NotInThisGame\
  Lists all friends other than those playing this game
* NotInGame\
  List all friends that are not currently playing a game
* AnyOnline\
  List all friends that are online
* AnyOffline\
  List all friends that are offline
* Away\
  List all online friends that are marked as away
* Buisy\
  List all online friends that are marked as buisy
* Followed\
  List the subset of friends that the local user follows, these may not be "friends" in the since that they may not have accepted a friend invite but are being followed by this player.

### Content

The transform where instantiated records will be parented to

### Record Template

This is a GameObject reference to a template or prefab. The Game Object must have a component on it that implements the [IUserProfile ](../interfaces/iuserprofile.md)interface.
