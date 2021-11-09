# Friend Manager

{% hint style="info" %}
This tool simply exposes common features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

## Definition

### Fields and Attributes

| Type | Name                    | Note                                  |
| ---- | ----------------------- | ------------------------------------- |
| bool | ListenForFrendsMessages | Should we listen for friend messages? |

### Events

#### evtGameConnectedChatMsg

Received a message from a friend

#### evtRichPresenceUpdated

Received a notfication of rich presence change

#### evtPersonaStateChanged

Received a notification of persona state change

### Methods

```csharp
public UserData[] GetFriends(flags);
```

Get lists of user friends, flags can be used to modify what subset is returned

```csharp
public UserData[] GetCoplayFriends();
```

Gets the list of friends the user has recently played with

```csharp
public string GetFriendMessage(userId, index, out type);
```

You should use this in responce to evtGameConnectedChatMsg to fetch the body of the message and the type of the message.
