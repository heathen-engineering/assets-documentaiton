---
description: Funcitonaly similar to Steam Client's Friends List
---

# FriendGroupsDisplay

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../../company/steam/">steam</a></td><td><a href="../../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../../physkit/">physkit</a></td><td><a href="../../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../../ux/">ux</a></td><td><a href="../../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

![](<../../../../../.gitbook/assets/image (176) (1).png>)

This control component is focused on emulation of Steam's own Friend List. It will read for and sort the local player's friends into the same list structure see in Steam Client's Friend List i.e. Playing, Online, Offline, any custom groups the player may have, etc.

This can be useful when you want a quick and easy UI element that the player is likely already familiar with.&#x20;

## Inspector Fields

### In Game Collection

This is a Transform which will be the root of all friends that are currently in or playing the current game.

### In Other Game Collection

This is a Transform which will be the root of all friends that are currently in or playing some other game.

### Grouped Collection

This is a Transform which will be the root of any custom groups the player may have defined.

### Online Collection

This is a Transform which will be the root of all friends that are currently online.

### Offline Collection

This is a Transform which will be the root of all friends that are currently offline.

### Group Prefab

This is a template or prefab that will be instantiated for each group found. i.e. Online, Offline, etc.

This GameObject must implement the [FriendGroup](friendgroup.md) component.

## Methods

### Clear

```csharp
public void Clear()
```

This simply destroys all loaded groups and profiles clearing the display. This is always called when the component is disabled.

### UpdateDisplay

```csharp
public void UpdateDisplay()
```

This simply rebuilds the display from scratch, that is it will first clear then re-construct the display insuring all elements are UpToDate. This is always called when the component is enabled.
