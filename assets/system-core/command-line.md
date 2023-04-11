---
description: Easy read of the commands passed in when your game was launched
---

# Command Line

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../company/steam/">Guides and Tutorials</a></td><td><a href="../steamworks/">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../company/steam/">steam</a></td><td><a href="../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../physkit/">physkit</a></td><td><a href="../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../ux/">ux</a></td><td><a href="../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

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
