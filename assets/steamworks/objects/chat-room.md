---
description: Represents a Clan Chat Room
---

# Chat Room

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../company/steam/">Guides and Tutorials</a></td><td><a href="../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../company/steam/">steam</a></td><td><a href="../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../physkit/learning/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../physkit/learning/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../physkit/learning/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../physkit/learning/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../physkit/">physkit</a></td><td><a href="../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../ux/">ux</a></td><td><a href="../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## Introduction

```csharp
public struct ChatRoom
```

The clan chat room structure is used by chat specific features of the Clans interface and is its self a shortcut to the most common chat features.

## Fields and Attributes

| Type                   | Name          | Comment                                                                                     |
| ---------------------- | ------------- | ------------------------------------------------------------------------------------------- |
| Clan                   | clan          | The clan this room belongs to                                                               |
| CSteamID               | id            | The id of the room                                                                          |
| EChatRoomEnterResponse | enterResponce | The responce from Steam when the user attempted to enter the room if any                    |
| UserData\[]            | Members       | The list of chat members, note client interface cannot iterate the full list of large clans |
| bool                   | IsOpenInSteam | Check if the chat is open in Steam UI                                                       |

## Methods

### Send Message

```csharp
public bool SendMessage(string message);
```

Attempts to send a message to the chat.

### Open Chat Window

```csharp
public bool OpenChatWindowInSteam();
```

Opens the clan chat in the Steam UI ... this is generally recomended especially for large clans as opposed to creating an in game clan chat.

### Leave

```csharp
public void Leave();
```

Leaves the clan chat if the user is in it
