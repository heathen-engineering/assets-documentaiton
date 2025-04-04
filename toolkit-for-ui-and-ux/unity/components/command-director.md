# Command Director



{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

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
