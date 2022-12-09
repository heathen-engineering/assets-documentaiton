# Stats and Achievements

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/concepts/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction&#x20;

<figure><img src="../../../../.gitbook/assets/image (1) (1) (2).png" alt=""><figcaption></figcaption></figure>

The Simple Achievements scene demonstrates reading and updating achievements using the AchievementObject. In this scene we use SetAchievementIcon, SetAchievementName and SetAchievementDescription components to populate the UI showing the icon, name and description of each achievement.

## Configuration

### Set Achievement Icon

Used on the RawImage to load the icon and update it based on changes to the achievement's state such as lock or unlock.

### Set Achievement Name

Used on the TextMesh Pro label to set the name of the achievement.

### Set Achievement Description

Used on the TextMesage Pro label to set the description on the achievement.

## Setting Value

Each of the UI elements shown on the screen is actually a Unity UI Toggle, when clicked it will set the value of the IsAchieved on the [AchievementObject ](../scriptable-objects/achievement-object.md)locking or unlocking it.

Note in this sample scene we do not call Store to commit the change so the changes wont commit until the app is closed. If you wanted to commit the changes before that you can call the Store method on any [AchievementObject ](../scriptable-objects/achievement-object.md)or StatObject to commit the changes now and this will cause the "popup" from Steam overlay to show if applicable.&#x20;

Steam Overlay doesn't work nicely in Unity Editor so we do not demonstrate that here.

### What About Stats?

They work much the same way with regards to setting the value, read the documentation on&#x20;

[Int Stat](../scriptable-objects/int-stat.md)

[Float Stat](../scriptable-objects/float-stat.md)

and [Average Rate Stat](../scriptable-objects/avg-rate-stat.md)

to learn more.

Stats do not have icons so there is no icon to load and each type of stat has its own "data type" but otherwise the process is the same, set the Valve of the stat and when ready call Store to commit the changes to the backend.
