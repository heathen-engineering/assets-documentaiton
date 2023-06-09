# Drag and Drop (Behaviours)

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../steam/steam.md">steam.md</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../core-concepts/">User eXperience Tools</a></td><td><a href="../ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

![](<../../../../.gitbook/assets/image (164) (1) (1) (1).png>)

This scene demonstrates the basics of the Drag and Drop system showing off the various drag and drop behaviours.&#x20;

### Return Home on clear

If the item is cleared e.g. droped out side of a valid drop container it will be sent to its "home" slot.  This can be useful for inventory systems which clearing an item from a character slot should return the item to the inventory.

### Return Previous on clear

This means the droped item will return to the previous valid slot or home if none when it is droped outside of a valid slot.

### Move Self

This means that the drag item which is clicked and dragged will be moved. If the item is cleared e.g. droped out side of a valid drop container it will be sent to its "home" slot.&#x20;

### Move Clone

This means that the drag item will clone its self and that the clone is what is moved not the original item. This is useful for spell books, shops and other cases where the original should remain fixed. The return home on clear in this case simply destroys the clone.

### Move Proxy

This means that a proxy object will be moved not the original ... e.g. while dragging some other icon or elements will follow the mouse, not the orignial item and not a clone of the original item. When droped in a slot the original item will be moved. This is useful for dragging items around the inventory so you can show a smaller less obstrusive element while dragging.

### Leave Proxy

This means that when dragging starts a proxy will be spawned in the place of the dragged item while the items its self is moved.

## What do I learn?

1. Setting up code free drag and drop
2. Setting up [drop containers](../../components/drop-container.md)
3. Setting up [drag items](../../components/drag-item.md)
4. Using the different drop and [drag behaviours](../../enums/drag-end-behaviours.md) and [effects](../../enums/drag-effect.md)
5. How to access the Knowledge Base (where you are now)
6. How to access the support [Discord ](https://discord.gg/6X3xrRc)
7. How to leave a review 😉

## Objects

You will see two columns in the UI each with 4 pair of [drop containers](../../components/drop-container.md), each pair having 1 [drag item](../../components/drag-item.md). Each pair is configured with a different combination of [Drag Effect](../../enums/drag-effect.md) and [Drag End Behaviour](../../enums/drag-end-behaviours.md). This is a simple demonstration of the result of each combination of effect and behaviour and has no custom scripts aside from the Knowledge Base, Discord and Leave a Review buttons.
