---
description: Easy read of the commands passed in when your game was launched
---

# Command Line

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

The CommandLine static class makes it easy to read the arguments passed in when your game was launched, and includes a set of common commands to help with common use cases.

## Examples

### Get Argument Line

This will return the string of arguments passed in as a single string

```csharp
string argumentLine = CommandLine.GetArgumentLine();
```

### Get Arguments

This will return an array of arguments and is similar to to calling `Environment.GetCommandLineArgs()` however it also handles WebGL and Android arguments on URL

{% hint style="info" %}
The array will be in the form of

`{ arg1, value1, arg2, value2, arg3, value3 }`
{% endhint %}

```csharp
string[] arguments = CommandLine.GetArguments();
```

### Get Steam Lobby Invite

A common use case that has been wrapped up as a simple 1 line call. This will return the id of the lobby the player has accepted the invite to, if any.&#x20;

```csharp
ulong lobbyId = CommandLine.GetSteamLobbyInvite();
if(lobbId == 0)
    //No lobby invite accepted
else
    //We have a lobby invite accepted and should join it
```

### Get Auto Config

A common use case that has been wrapped up as a simple 1 line call. This will return true if the SteamAutoConfig argument has been passed in.&#x20;

Auto Configure is a feature many gamers expect exists in a game. It was originally part of the Source engine (Valve's engine they built HL2 and various other games on). When this is detected the gamer is expecting the game to reset its graphics settings and is most often used when the game's configuration causes a fatal error on load.

```csharp
if(CommandLine.GetAutoConfig())
    //We should default the graphics settiings
```
