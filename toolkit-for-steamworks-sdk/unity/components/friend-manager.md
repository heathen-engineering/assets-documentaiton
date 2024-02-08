---
cover: ../../../.gitbook/assets/Unity Banner@2x.png
coverY: 0
---

# Friend Manager

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="info" %}
This tool simply exposes common features present in the API to the inspector.



This is not required to use these features it is simply a helper tool allowing user's who are more comfortable working with editor inspectors and game object rather than classic C# objects and scripting to make use of the related feature.
{% endhint %}

### Namespace

```csharp
using HeathenEngineering.SteamworksIntegration;
```

### Definition

```csharp
public class FriendManager : MonoBehaviour
```

## Events

### evtGameConnectedChatMsg

```csharp
public GameConnectedFriendChatMsgEvent evtGameConnectedChatMsg
```

Received a message from a friend, this willy be raised if you first set the [ListenForFriendsMessages](friend-manager.md#undefined) to true.

The handler for this event would look like the following.

```csharp
public void HandleFriendChatMsg(UserData friend, 
        string message, 
        EChatEntryType type)
{
        //Do Work
}
```

You can see the various options for [EChatEntryType](https://partner.steamgames.com/doc/api/steam\_api#EChatEntryType) in Valve's documentation as linked.

### evtRichPresenceUpdated

```csharp
public FriendRichPresenceUpdateEvent evtRichPresenceUpdated
```

Received a notfication of rich presence change

The handler for this event would look like the following

```csharp
public void HandleRichPresenceUpdated(FriendRichPresenceUpdate_t update)
{
    //Do Work
}
```

The [FriendRichPresenceUpdate\_t](https://partner.steamgames.com/doc/api/ISteamFriends#FriendRichPresenceUpdate\_t) structure is defined in Steamworks namespace space and discribes the friend ID and AppId related to the event.

### evtPersonaStateChanged

```csharp
public PersonaStateChangeEvent evtPersonaStateChanged
```

Received a notification of persona state change

The handler for this event would look like the following

```csharp
public void HandlePersonaStateChanged(PersonaStateChange_t stateChange)
{
    //Do Work
}
```

The [PersonaStateChange\_t](https://partner.steamgames.com/doc/api/ISteamFriends#PersonaStateChange\_t) structure is defined in the Steamworks namespace and discribes the user the change is related to as well as the changes.

## Fields and Attributes

### ListenForFriendsMessages

```csharp
public bool ListenForFriendsMessages { get; set; }
```

This indicates rather or not the system is listening for freind chat messages. Note that friend chat messages will only be raised in game if you set this to true.

## Methods

### Get Friends

```csharp
public UserData[] GetFriends(EFriendFlags flags);
```

Get lists of user friends, The flags argument is of type [EFriendFlags](https://partner.steamgames.com/doc/api/ISteamFriends#EFriendFlags) and can be used to modify what subset is returned.

This is the same as calling `API.Friends.Client.GetFriends(flags);`

### Get Coplay Friends

```csharp
public UserData[] GetCoplayFriends();
```

Gets the list of friends the user has recently played with

### Get Friend Message

```csharp
public string GetFriendMessage(UserData userId,
               int index,
               out EChatEntryType type);
```

You should use this in responce to evtGameConnectedChatMsg to fetch the body of the message and the type of the message.

You shouldn't need to call this as we will call it for you and raise the [evtGameConnectedChatMsg](friend-manager.md#evtgameconnectedchatmsg) with the results.

### SendMessage

```csharp
public bool SendMessage(UserData friend, string message);
```

Sends the target friend a string message. If this returns false it means the local user is rate or chat limited by Valve and cannot send a message.

## How To

### Create an in-game Friends List

The UI work is left up to you ... the following code will demonstrate fetching friends and how you might read the data contained within.

Note that the "Immediate" flag is your "normal" friends such as what you see in your Steam Client's friend list.

```csharp
UserData[] friends = friendManager.GetFriends(EFriendFlags.k_EFriendFlagImmediate);
```

Now that we have an array of our friends we can simply iterate over that and populate our UI

```csharp
foreach(UserData friend in friends)
{
    //freind.Name;
    //friend.Avatar;
    //etc.
}
```

Be sure to read and understand all the features of the [UserData](../classes-and-structs/user-data.md) object. You can also use tools like [SetUserAvatar ](../ui-components/set-user-avatar.md)and [SetUserName ](../ui-components/set-user-name.md)to simplify fetching and keeping up to date the friend's avatar image and display name.

### Create an in-game Friend Chat

The UI work is left up to you ... the following code will demonstrate enabling friend chat, listening for chat messages and sending messages to that friend.

First we should set up our event handler to listen for friend chat messages. You can do this in the Unity inspector or in code.

```csharp
friendManager.evtGameConnectedChatMsg.AddListener(HandleChatMsg);
```

The handler for that would look like this

```csharp
private void HandleChatMsg(UserData friend, string message, EChatEntryType type)
{
    if(type == EChatEntryType.k_EChatEntryTypeChatMsg)
    {
        //We got a messaage from friend.Name so display it
    }
}
```

In the above example we are only paying attention to chat message types of ChatEntry. You can see all the different types [here and what they mean](https://partner.steamgames.com/doc/api/steam\_api#EChatEntryType).

Before the system will raise the evtGameConnectedChatMsg event we need to tell it to listen for messages.

```csharp
friendManager.ListenForFriendsMessages = true;
```

Finally in order to send a friend a chat message we use the UserData of that friend. Lets assume we have a UserData named friend and that is who we want to send the message to.

```csharp
friend.SendMessage("Hello Friend");
```

We could also send the message via the friendManager such as&#x20;

```csharp
friendManager.SendMessage(friend, "Hello Friend");
```

This is simply an example you would of course want to give the user a means to input text to send to your friend so you would likely drive this from a InputField's on submit or similar.
