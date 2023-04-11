---
description: Simple chat made simple
---

# Lobby Chat Director

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th></th><th></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><h2>Steam</h2></td><td><a href="../../../../company/steam/">Guides and Tutorials</a></td><td><a href="../../">Integration (Unity and Godot)</a></td><td></td><td></td><td><a href="../../../../company/steam/">steam</a></td><td><a href="../../../../.gitbook/assets/Steamworks Card.png">Steamworks Card.png</a></td></tr><tr><td><h2>PhysKit</h2></td><td><a href="../../../physkit/sample-scenes/fantasy-style-ballistic-simulation.md">Ballistics</a></td><td><a href="../../../physkit/sample-scenes/1-buoyancy-example.md">Buoyancy</a></td><td><a href="../../../physkit/sample-scenes/1-force-effect-fields.md">Force Effects</a></td><td><a href="../../../physkit/sample-scenes/2-verlet-spring-skinned-mesh.md">Verlet (Physics Bone)</a></td><td><a href="../../../physkit/">physkit</a></td><td><a href="../../../../.gitbook/assets/PhysKit Card.png">PhysKit Card.png</a></td></tr><tr><td><h2>UX</h2></td><td><a href="../../../ux/learning/core-concepts/">User eXperience Tools</a></td><td><a href="../../../ux/learning/ugui-extras/">uGUI Extras</a></td><td></td><td></td><td><a href="../../../ux/">ux</a></td><td><a href="../../../../.gitbook/assets/Splash Screen (1).png">Splash Screen (1).png</a></td></tr></tbody></table>

## &#x20;Introduction

{% hint style="info" %}
This tool simply exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

The Lobby Chat Director must be attached to a Lobby Manager. The director simply exposes lobby chat features to the Steam Inspector.

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class LobbyChatDirector : MonoBehaviour
```

## Events

### evtMessageRecieved

```csharp
public LobbyChatMsgEvent evtMessageRecieved
```

Occurs when a chat message is received on this lobby, The handler for this event would take a form similar to.

Uses the [LobbyChatMsg](../../objects/lobby-chat-msg.md) object

```csharp
private void Handler(LobbyChatMsg arg)
{
    //Handle the message
}
```

## Fields and Attributes

### HasLobby

```csharp
public bool HasLobby => get;
```

## Methods

### Send

```csharp
public bool Send(string message);
```

```csharp
public bool Send(byte[] data);
```

```csharp
public bool Send(object jsonObject);
```

Sends the related data to the lobby chat.

The total length of the message regardless of datatype must be less than 4kb in size. When sending a jsonobject Heathen will use Unity's JsonUtility to convert the object to a JSON string and then use UTF8 encoding to convert that to a byte\[] before sending.&#x20;

## Use

### Simple Chat

The most common use case for Lobby Chat is as a simple text based chat system. In this model your users would typically if not always be sending string data. You would simply listen on the [evtMessageRecieved ](lobby-chat-director.md#evtmessagerecieved)such as&#x20;

```csharp
private void HandleMessage(LobbyChatMsg message)
{
    Debug.Log(message.sender.Name + " sent a message: " + message.Message);
}
```

The above simply demonstrates a valid handler; you would of course want to display that message to your users. You can do this with whatever UI system you choose to use that part is up to you.

See the [Lobby Chat Msg](../../objects/lobby-chat-msg.md) object article for more information on what you can find in the message paramiter.

### Advanced Chat

You may have notiiced that the Lobby Chat Director can send an object over the chat channel. This object must be serializable by UnityEngine.JsonUtility. What happens is that Heathen's system will use the JsonUtility and the UTF8 encoding tool in .NET to convert your object to a byte\[] for sending.

You can create your own serializable object type such as a class or struct and send that via the Send method. When you recieve a message you can fetch that type using the FromJson member.

```csharp
private void HandleMessage(LobbyChatMsg message)
{
    var myObject = message.FromJson<MyCustomType>();
}
```

You can get as clever or remain as simple as you like with this system. For example you could use class inheritance to determin the data type of a message or you could simply assume that any message that starts with the { character is a JSON string and so should be read via the FromJson.

You can see more examples and sample code in the Samples section of the asset.
