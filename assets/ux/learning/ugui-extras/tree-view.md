---
description: Simple GameObject driven tree view control for uGUI
---

# Tree View Collection

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../steam/steam.md">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../steam/steam.md">steam.md</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../core-concepts/">User eXperience Tools</a></td><td><a href="./">uGUI Extras</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

The tree view is a common GUI element that Unity simply lacks and isn't trivial to create from scratch. The Tree View Collection component simplifies this and makes it easy to manage tree views by expressing the data of the collection as GameObjects in your scene hierarchy.

Put more simply, the Tree View Collection will manage a the children of a targeted GameObject creating a Tree View UI element that is easy to create, read and manage.

### Tree View Collection

This represents the collection its self and can be treated similar to a Unity uGUI Layout control though doesn't control the layout position rather this will control the parentage of the objects its managing.

{% hint style="info" %}
To affect the position layout such as to cause child nodes to organize themselves in a vertical layout then you should use Unity's built-in features such as Vertical Layout.
{% endhint %}

#### Node Prototype

This is the prefab that should be instantiated to represent your nodes in your game's UI. The prototype should implement the **Tree View Node** component.

#### Root

This is the root where the Tree View Collection will create and manage nodes.

### Tree View Node

This component represents the visual node as it will appear in your UI. The typical approach is to define this prototype in scene in a disabled GameObject as a template. This is a similar approach to Unity's own DropDown and its Template.

![](<../../../../.gitbook/assets/image (129).png>)

The available fields are

#### Tree

This should be set to the parent tree. If you use the Template approach as discribed here you can set this at development time. If you do not then you will need to set this value at run time when you instantiate the object.

#### Parent

This will be set by the Tree View that is controlling this node and managed as the node is moved up and down in the structure.

#### Content

This is the RectTransform under which the visual representation for the node its self would live e.g. the label, a toggle if you like, etc.

#### Collection

This is the RectTransform under which child nodes will be placed. When this node is "collapsed" this GameObject is set inactive hiding the children.

#### Is Expanded

This simply indicates rather or not this node is expanded e.g. is its children visible.

## Configuration

### Tree View Collection

![](<../../../../.gitbook/assets/image (130).png>)

The Tree View Collection is the root of the system and would typically be placed above Unity layout controls such as Scroll Views, Vertical Layout, etc.&#x20;

The two fields of the Tree View Collection must be populated for the control to work. See the Tree View Collection notes above for information on each.

Once you have created and configured the structure you can use the Editor control's "+ Create Child" button to create a root node if desired.

### Tree View Node

![](<../../../../.gitbook/assets/image (132).png>)

The Tree View Node is the "element" of the Tree View Collection and will be instantiated for each node in the collection.

The core fields to configure on your prototype would be

* Tree\
  This is the parent tree and used for all collection wide features.
* Content\
  This is the root of the node's visual representation e.g. the objects under this point are the label, icon, toggle, etc. that visually express this node in your UI
* Collection\
  This is the root where children of this node will be placed. Typically it would include a Vertical Layout to organize the children in a meaningful way.

## Code Examples

{% hint style="warning" %}
TreeViewCollection is a proper .NET ICollection object meaning it can be used with features such as&#x20;

```csharp
foreach(var node in collection)
{
    //This walks the root nodes of the tree
}
```
{% endhint %}

### Walk the Tree

This means to iterate over each node in the tree. The tree its self you can easily walk the root nodes with .NET's foreach command as shown in the tip above. To perform a walk across all nodes requires a bit of extra work.

```csharp
...
foreach(var node in treeViewCollection)
{
    WalkANode(node);
}
...

private void WalkANode(TreeViewNode node)
{
    foreach(var child in node)
    {
        //Walk our grand children
        WalkANode(child);
        
        //Do whatever we need to do on this node
    }
}
```

### Get Node Count

You can get the count of the nodes contained directly in the tree e.g. the root nodes via

```csharp
var result = collection.Count;
```

you can get the count of the nodes under a given node via

```csharp
var result = node.Count;
```

You can get the count of all nodes in the collection including children via

```csharp
var result = collection.Count;
foreach(var node in collection)
    result += node.Count;
```

### Create Node

To create a new default node ready for addition to the tree you have two options. These examples require a reference to the Tree View Collection.

```csharp
var node = collection.CreateNode();
```

```csharp
var node = collection.CreateNode(parentNode);
```

If no parent node is provided the new node will made a child of the tree its self e.g. a "root" node.

### Add a Node

To add a node to the collection its self

```csharp
collection.Add(node);
```

To add a node to an existing node

```csharp
node.Add(newNode);
```

### Remove a Node

{% hint style="danger" %}
Removing a node destroys it, if you want to pop the node off or move it then use the move commands or reparent it.
{% endhint %}

To remove a node from the tree its self

```csharp
collection.Remove(node);
```

To remove a node from a node

```csharp
node.Remove(otherNode);
```

### Clear Nodes

You can clear all nodes via

```csharp
collection.Clear();
```

You can clear the children from a given node via

```csharp
node.Clear();
```

### Move Up

This moves a node up to be above the next sibling

```csharp
node.MoveUp();
```

### Move Down

This moves a node down to be below the next sibling

```csharp
node.MoveDown();
```

### Promote

This moves a node higher in the hierarchy e.g. becomes a sibling of its parent

```csharp
node.Promote();
```

### Demote

This moves a node lower in the hierarchy e.g. becomes a child of the sibling above it

### Copy To Array

This is a common feature of all ICollection objects in .NET and copies the contents of the collection into a standard array from the index provided. The array passed in must be large enough to hold the collection. The index represents the index at which the copy will start.

For example if you passed in an array with a length of 100 and passed in an index of 10 the operation will fail to copy if the tree has more than 90 entries since the copy will start at the 10th index and move forward from that point.

```csharp
collection.CopyTo(array, index);
```
