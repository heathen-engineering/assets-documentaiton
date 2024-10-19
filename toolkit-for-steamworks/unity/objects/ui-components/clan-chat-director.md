---
cover: ../../../../.gitbook/assets/Unity Banner.jpg
coverY: 0
---

# Clan Chat Director

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

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

### Members

```csharp
public UserData[] Members => get;
```

The members seen in this chat room, this may not list all members for large chat rooms.

### Is Open In Steam

```csharp
public bool IsOpenInSteam => get;
```

This will be true if the Clan chat window is open in the Steam Friend Chat dialog of Steam.

### In Room

```csharp
public bool InRoom => get;
```

This will be true if the user is "in" this chat room

### Chat Room

```csharp
public ChatRoom ChatRoom => get;
```

The chat room associated with this director if any

## Events

### evtJoin

```csharp
public GameConnectedChatJoinEvent evtJoin;
```

Occurs when a member joins the room

### evtRecieved

```csharp
public GameConnectedClanChatMsgEvent evtReceived;
```

Occurs when a message is received to this room

### evtLeave

```csharp
public GameConnectedChatLeaveEvent evtLeave;
```

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

