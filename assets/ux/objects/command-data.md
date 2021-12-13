# Command Data

## Introduction

{% hint style="info" %}
Part of the [Command System](../learning/core-concepts/command-system.md) of the UX Foundation and UX Compelete assets
{% endhint %}

Represents a command and its related data. This can be used to convert any string into a refernce to the related commannds GameEvent and to extract the arguments from the command if any.

### Fields and Attributes

### isValid

Indicates the command is valid, if false other fields will be null and this command can be ignored.

### command

A reference to the related [GameEvent](../../system-core/game-events.md) if valid.

### sourceText

The text that was parsed to find this command, this may contain additional commands.

### arguments

The part of the text that follows the command if any

## Constructor

```csharp
public CommandData(CommandLibrary library, string command, bool userOnly)
```

This constructor takes a refernce to a [Command Library](command-library.md) and will parse the provided text to construct the resulting command.
