# Clan Chat Director

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

The Clan Chat Director is intended to be attached to your Clan/Group chat UI. You will then need to call the Join method to connect the director to a specific clan's chat. Assuming the user is permitted to be in that chat you will now start receiving messages from that chat and send messages to that chat.&#x20;

For smaller groups/clans you can also iterate over the members of the chat however be advised that most Steam groups / clans get very large and cannot be iterated over by the user.

## Definition

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class ClanChatDirector : MonoBehaviour;
```

## Fields and Attributes

|             |               |                                                                                                                                                                                                                            |
| ----------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UserData\[] | Members       | Returns the members in this chat room if the user is able to iterate over them.                                                                                                                                            |
| bool        | IsOpenInSteam | True if the clan chat is open in Steam client or oen of its dialogs                                                                                                                                                        |
| bool        | InRoom        | <p>True if the system has been connected to a room succesfuly.</p><p></p><p>Note it is possible to be removed a room and this not be updated. You should handle errors when attempting to send and adjust accordingly.</p> |
| ChatRoom    | ChatRoom      | <p>Returns the ChatRoom object that is being operated on if any.</p><p></p><p>If none then this will return a default ChatRoom with an invalid ID</p>                                                                      |

## Events

### evtJoin

Occurs when a member joins the room

### evtRecieved

Occurs when a message is received to this room

### evtLeave

Occurs when a member leaves the room

## Methods

### Join

```csharp
public void Join(Clan clan);
```

Joins the chat for the indicated clan

### Leave

```csharp
public void Leave();
```

Leaves the chat if present

### Send

```csharp
public bool Send(string message);
```

Sends a chat message if present

### Open in Steam

```csharp
public void OpenInSteam();
```

Opens the clan chat in Steam's overlay or chat dialog

