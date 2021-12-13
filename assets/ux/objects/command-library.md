# Command Library

## Introduction

{% hint style="info" %}
Part of the [Command System](../learning/core-concepts/command-system.md) of the UX Foundation and UX Compelete assets
{% endhint %}

A scriptable object referencing a set of commands and details about how those commands are to be parsed. A command is simply a [GameEvent](../../system-core/game-events.md) that can be looked up by name. Your game can then listen for these game events to know when a command was ran. This system also handles paramiterizezd commands, that is the arguments following a command can be parsed and sent along with it.

```csharp
/emote wave
```

This might be parsed to invoke a Game Event named `emote` and pass a string argument of `wave` you can then handle this event and use the argument to determin what animation to play in the case of an emote system.

### Fields and Attributes

### useCaseSinsativeCommandNames

When parsing should case be respected

```csharp
public bool useCaseSinsativeCommandNames = false;
```

### commandStartString

What token should be watched for when searching strings for commands

```csharp
public string commandStartString = "/";
```

### developerCommands

Commands identified as "developer" commands, when parsing you can filter out developers commands. When used these are usually commands that are not restrectied from player access but require an additional layer of effort on the player's part similar to "console commands" in games like Elder Scrolls or Fallout.

If you want to prevent players from running a command, do not innclude it in your released game. If you do include a command in your game your players will find a way to run it.

```csharp
public List<GameEvent> developerCommands
```

### userCommands

Commands identified as "user" commands, when parsing. User commands are always searched when parsing and are in constrast to "developer" commands.

```csharp
public List<GameEvent> userCommands
```

## Methods

### TryParseCommand

Attempts to match the input string to a command optionally filtering on user commands only

```csharp
public bool TryParseCommand(string inputString, 
                            bool userOnly, 
                            out GameEvent gameEvent, 
                            out string argument)
```

### TryCallCommand

Attempts to match the input string to a command and to raise the matching command event with the provided arguments

```csharp
public bool TryCallCommand(string inputString, 
                           bool userOnly, 
                           out string errorMessage)
```

### VerifyCommand

Returns true if the provided string is a command

```csharp
public bool VerifyCommand(string inputString, 
                          bool userOnly, 
                          out string errorMessage)
```

### ParseCommand

parses a command and returns the [Command Data](command-data.md).

```csharp
public CommandData ParseCommand(string inputString, bool userOnly)
```
