---
description: Simple chat made simple
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Lobby Chat Director

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
This tool exposes features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing users who are more comfortable working with editor inspectors and game objects rather than classic C# objects and scripting to make use of the related feature.
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

Uses the [LobbyChatMsg](../classes/lobby-chat-msg.md) object

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

The most common use case for Lobby Chat is as a simple text-based chat system. In this model, your users would typically if not always be sending string data. You would simply listen on the [evtMessageRecieved ](lobby-chat-director.md#evtmessagerecieved)such as&#x20;

```csharp
private void HandleMessage(LobbyChatMsg message)
{
    Debug.Log(message.sender.Name + " sent a message: " + message.Message);
}
```

The above demonstrates a valid handler; you would want to display that message to your users. You can do this with whatever UI system you use that part is up to you.

See the [Lobby Chat Msg](../classes/lobby-chat-msg.md) object article for more information on what you can find in the message parameter.

### Advanced Chat

You may have noticed that the Lobby Chat Director can send an object over the chat channel. This object must be serializable by UnityEngine.JsonUtility. What happens is that Heathen's system will use the JsonUtility and the UTF8 encoding tool in .NET to convert your object to a byte\[] for sending.

You can create your own serializable object type such as a class or struct and send that via the Send method. When you receive a message you can fetch that type using the FromJson member.

```csharp
private void HandleMessage(LobbyChatMsg message)
{
    var myObject = message.FromJson<MyCustomType>();
}
```

You can get as clever or remain as simple as you like with this system. For example, you could use class inheritance to determine the data type of a message or you could simply assume that any message that starts with the { character is a JSON string and so should be read via the FromJson.

You can see more examples and sample code in the Samples section of the asset.
