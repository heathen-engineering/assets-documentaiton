# Command Director



{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/concepts/steam/">Guides and Tutorials</a></td><td><a href="../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/concepts/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/1-ballistic-basics.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../learning/core-concepts/">User eXperience Tools</a></td><td><a href="../learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../">..</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

{% hint style="info" %}
Part of the [Command System](../learning/core-concepts/command-system.md) of the UX Foundation and UX Compelete assets
{% endhint %}

Changes the configured Default State for the Cursor system.

## Events

### evtCommandFound

Occurs when a command is found in parsed text and provides a refernce to the found command.

You would add a listener on this event via theUnity inspector as you would for other Unity events or in code such as:

Assuming a handler in the form of

```csharp
private void HandleEvent(CommandData command)
{
}
```

Then you would register the event such as:

```csharp
commandDirector.evtCommandFound.AddListener(HandleEvent);
```

When you no longer need this handler you should remove it for example when the behviour using it is destroyed

```csharp
void OnDestroy()
{
    commandDirector.evtCommandFound.RemoveListener(HandleEvent);
}
```

## Fields and Attributes

### Library

```csharp
public CommandLibrary library;
```

A reference to the [command library](../objects/command-library.md) to be used

### UserOnly

```csharp
public BoolReference userOnly;
```

Should this directory handle user only commands

## Methods

### ParseInput

Parses an input string and raises the command found event as required. This is most offten used with UI integrations such as a player console or chat box.

```csharp
public void ParseInput(string value);
```

### ParseCommand

Parses an input string and returns the command data found. This is a more direct solution and doesn't trigger the evtCommandFound. You will need to handle the [CommandData ](../objects/command-data.md)your self.

```csharp
public CommandData ParseCommand(string value);
```
