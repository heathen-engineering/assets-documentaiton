---
description: >-
  Parse commannds from players and invoke corresponding GameEvents to drive
  emotes, help systems and macro systems and more.
---

# Command System

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="./">User eXperience Tools</a></td><td><a href="../ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../">..</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

The Command System works with System Core's [GameEvents ](../../../system-core/game-events.md)to enable an easy to use and flexible command system for your next project. Commands can be parsed from string input and used to invoke game events on demand with or without arguments. This can be used for simply player commands such as emotes, chat whisper, help commands, etc. or used to drive more complex systems such as macros and end user scripting.

### How does it work?

Create your commands as [GameEvents ](../../../system-core/game-events.md)in your asset database, the name of the event will be used as its command text. You can use String Game Event to pass the arguments of a command along with it or you can use the Command Director to parse arguments ahead of time and use more complex or even custom Game Events with detailed parameters.

Once you have your [GameEvents ](../../../system-core/game-events.md)defined you link them to a Command Library this represents the set of commands the system will listen for and defines how the commands will be identified. The Command Library can be used to parse through any text searching for matching commands and optionally invoke any command found. You can also use tools such as the Command Director to pass command data into your own systems where you can perform additional logic such as parsing arguments for more complex commands.

## Configuration

Step 1 is always to define your commands. A command is simply a [GameEvent](../../../system-core/game-events.md) and you can use any type of [GameEvent](../../../system-core/game-events.md) you want even custom [GameEvents](../../../system-core/game-events.md). To learn more about what a [GameEvent ](../../../system-core/game-events.md)is please read the [Knowedge Base articles on System Core's GameEvents](../../../system-core/game-events.md).

Once you have defined your commands your next step is to reference them in your Command Library. A command library is Scriptable Object that lists all the valid commands and how they should be parsed. You can create a new Command Library in your asset folders by right clicking and selecting **Create > UX > Commands > Library.**

With your library populated your ready to use the system as is, additional tools such as the Command Director are described below.

## Command Library

This object acts as a collection of valid commands and provides the basic logic for parsing text and matching commands.

![](<../../../../.gitbook/assets/image (133).png>)

You can create a new Command Library by right clicking in your asset folder and seleting Create > UX > Commands > Library.

Command Library's fields are&#x20;

### Use Case Sensitive Command Names

As the name suggests if this is true the system will require the case of the input string to match the name of the GameEvents used as commands.

### Command Start String

This is the string that is tested for at the start of input to determine if a command follows. It must be the start of the input string or the input will be ignored e.g.

```
"echo this is my message"
```

```
" /echo this is my message"
```

```
"Hi /echo this is my message"
```

None of the above strings would not result in the echo command being invoked however

```
"/echo this is my message"
```

The above text shown here however will match a command named Echo or echo and will pass "this is my message" as the argument.

{% hint style="info" %}
Notice that the space between the command name and the message is removed. The parsing system looks for the start string and ends at the first space.

Command names **can** contain spaces e.g. a GameEvent named "My Command" is a valid name however it might be confusing to your users as the command for it with an argument would look like this&#x20;

```
"/my command This is my argument"
```
{% endhint %}

### Developer Commands

A list of [GameEvents ](../../../system-core/game-events.md)representing privileged commands.&#x20;

{% hint style="info" %}
Note this is not a security features its more akin to splitting out the commands you might use in a developer console such as seen in Skyrim or similar vs commands that work everywhere or in common places such as in a MMO's chat box.
{% endhint %}

The command system can be useful for developers, moders and other cases where perhaps the regular end user shouldn't have unrestricted access to the commands. When parsing for commands you can enable or disable checking for all or user only commands this simply means the parse will or will not check the Developer Commands as well as the User Commands. Note if a command matches in both the Developer Command will be taken first if enabled.

### User Commands

A list of [GameEvents](../../../system-core/game-events.md) representing regular commands.

## Command Director

This object is simple helper tool that can help you direct input text to the Command Parser and raise an event containing the results of the parse. The main feature of this object is the **Evt Command Found** event this will be invoked with each successful parse and contains details about the command and arguments found, useful for more complex command uses where you need to apply your own logic before the command is invoked.

A typical use case is to use the OnEndEdit of a standard InputField and connect it to the Command Director's `ParseInput` function.&#x20;

The fields of the director include

### Library

This is a reference to the library that should be used for command parsing

### User Only

This indicates rather or not the director should test for user only or both user and developer commands

### Evt Command Found

This is an event which is raised when a valid command is parsed

## Command Data

Command data is the object sent when the Command Directory raises its Evt Command Found. Put more simply its the type of data sent in the parameter of that event.&#x20;

Command Data has the following fields

### Is Valid

Indicates rather or not the command is a valid command

### Command

A reference to the GameEvent the command matched with

### Arguments

The string following the command text e.g. its arguments. Its up to you to parse this if you want to extract more specific information such as converting it to numbers, splitting multiple parameters out, etc.

### Source Text

The string that was parsed to find this information

## Advanced Concepts

### Nested Commands

You can enable nested commands by handling the results of the Command Director and calling it again on the argument string. Depending on your needs you may want to parse the arguments manually e.g. search for occurrences of where a space is followed by the command start string e.g. something similar to

```csharp
var commandList = input.Split(", ");
```

#### When would use it?

```
/macro /targetPet, /e pet
```

This suggests a macro system that is able to take as input multiple commands. You can imagine this might let a user create a button that lets the target there own pet and then perform the pet emote. Macro systems typically work by giving the users a set of modular commands such as targeting commands, emotes, etc that they can string together to perform more complex actions. In this case macro is a command your system is using to understand that the arguments is such a set of modular commands which are them selves commands the Command Directory can parse for ... once you split them apart as desired.

## Code Examples

### Parsing Commands

You have multiple ways to parse commands, the most basic is to use the Command Library directly

```csharp
if(library.TryParseCommand(inputString,
                           userOnly,
                           out GameEvent command,
                           out string arguments))
{
   //If we get here then command is the game event
   //arguments is the string that follows it
}
```

The library can also call commands directly e.g. it will parse it as seen above and if found it will go ahead and invoke it if it can.

```csharp
if(library.TryCallCommand(inputString,
                          userOnly,
                          out string errorMessage))
{
    //If we get here then we called a command
}
else
{
    //If we get here we did not call a command ... check errorMessage for details
}
```

The TryCallCommand feature is "smart" that is if it finds a command it will check the command type and if the type is something other than void it will attempt to parse the arguments accordingly. Supported types include

* GameEvent\
  This is the void game event type e.g. ignores the arguments
* StringGameEvent\
  This will pass the arguments in to the event as a string
* IntGameEvent\
  This will attempt to parse the arguments to an int
* FloatGameEvent\
  This will attempt to parse the arguments to a float
* BoolGameEvent\
  This will attempt to parse the arguments to a bool
* DoubleGameEvent\
  This will attempt to parse the arguments to a double

Finally you can use the ParseCommand option available on both the Command Library and on the Command Director ... or optionally directly from the CommandData object as a constructor.

```csharp
var commandData = library.ParseCommand(inputString, userOnly);
```

```csharp
var commandData = director.ParseCommand(inputString);
```

```csharp
var commandData = new CommandData(library, inputString, userOnly);
```

### Using Command Data

Command Data is the object passed by the Command Director's Evt Command Raised event and can be constructed directly by your own logic with a simple single line call as shown the Parsing Commands example above.

Once you have a Command Data object you can use it to invoke the GameEvent represented by the command and to handle any arguments the command might have included.

```csharp
//Is this command valid?
if(data.isValid)
    Debug.Log("Yes it is");
else
    Debug.Log("No it is not");
```

```csharp
//What game event does this command use
var gameEvent = data.command;
```

```csharp
//What arguments came with the command
var arguments = data.arguments;
```

```csharp
//What was the source of the command (its input string)
var source = data.sourceText;
```

### Invoking Command Data

Invoking command data will depend on what kind of command it is. Knowing what type of command it is, is best done by you at development time e.g.&#x20;

{% hint style="info" %}
You will notice that we always pass "this" as the first paramiter with any game event. The concept here is taken from .NET's standard approch to event deligates it simply tells the listener who the caller of the event was, this is particularly useful for GameEvents since they can be invoked by a wide array of sources and you may want to handle each differently ...&#x20;

```csharp
publiv void HandleGameEvent(object source)
{
    if(source == myDirector)
     ;//Do something about it
    else if (source == myLibrary)
     ;//Do something about it
}
```
{% endhint %}

```csharp
switch(data.command.name)
{
    case "void":
        Debug.Log("I know I created this as a GameEvent ... no need to cast here");
        data.command.Invoke(this);
    break;
    case "echo":
        Debug.Log("I know I created this as a StringGameEvent");
        ((StringGameEvent)data.command).Invoke(this, data.argument);
    break;
    case "someOtherCommand":
        Debug.Log("I know I created this as something :)");
    break;
    ... etc ...
}
```
