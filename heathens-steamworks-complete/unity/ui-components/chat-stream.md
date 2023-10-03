---
cover: ../../../.gitbook/assets/Unity Banner@4x-100.jpg
coverY: 0
---

# Chat Stream

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Displays a flow of chat messages such as those received from the [Clan Chat Director](clan-chat-director.md) or [Lobby Chat Director](lobby-chat-director.md).

```csharp
namespace HeathenEngineering.SteamworksIntegration.UI
```

```csharp
public class ChatStream : MonoBehaviour
```

## Fields and Attributes

### History Length

{% code fullWidth="false" %}
```csharp
[SerializeField]
private uint historyLength = 200;
```
{% endcode %}

How many chat entries should the tool maintain. When the count exceeds this number the oldest message will be destroyed. This is important for managing total memory use and keeping Unity UI from getting out of hand with long or fast running chats.

### Content

```csharp
[SerializeField]
private Transform content;
```

The root where chat messages will be spawned as they come in

### Message Template

```csharp
[SerializeField]
private GameObject messageTemplate;
```

The object that will be cloned / instantiated for each received message. This should contain a component in the root of the template that implements the [IChatMessage](../programming-tools/ichatmessage.md) interface.

## Methods

### Handle Clan Message

```csharp
public void HandleClanMessage(ClanChatMsg message)
```

Used by the [Clan Chat Director](clan-chat-director.md) to apply a clan chat message

### Handle Lobby Message

```csharp
public void HandleLobbyMessage(LobbyChatMsg message)
```

Used by the [Lobby Chat Director](lobby-chat-director.md) to apply a lobby chat message

### Handle Message

```csharp
public void HandleMessage(UserData sender, string message, EChatEntryType type)
```
