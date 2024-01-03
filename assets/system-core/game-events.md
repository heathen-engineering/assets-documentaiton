---
description: System Core Game Events
---

# Game Events

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Game Events are simply Scriptable Objects stored in your Unity asset folder which can act like events being "listened to" by funcitons throughout your game and invoked by actions in your game.&#x20;

**Why Though?**

Why not just use Unity Events or better still proper .NET deligates? Well actually Heathen's Game Events do use both Unity Events and deligates under the hood but making them Scriptable Objects means you can define these events as part of your game's asset database. This inturn means they can be referenced at development time or run time across any scene and with no worry about rather or not they are loaded as they are loaded with the game its self.

Game Events are ideal for any sort of global event of which most games have quite a few. Some examples uses follow.

**Common Events**\
Classicly pressing F1 on your keyboard should pull up a help menu ... go ahead try it right now and whatch your browser open its help interface. This should happen no matter where you are in a game or what is going on so doing this in a traditiona game without a global event system such as Game Events makes this very hard to do.

There are other such events and generally this will depend on what platform your on. In PC F1 is help, in mobile swipe up should open the system menu, in consoles we offten have a pause or menu button, etc. and in games in general player's have some expectations based on genre or other common factors that might fit well as a Game Event.

**Game Input**\
By this we mean inputs from the player to the game ... not your fictional world or its character but inputs such as Pause, Resume, System Settings, Return to Menu and anything else that should take precedence over the state of your game. Doing this up as Game Events greatly reduces the maintenance required and helps insure you dont end up with gaps where these inputs just arn't handled such as switching between scenes and similar.

**System Events**\
These are events that drive from the system its self, bare bones there should be in every program an Unhandled System Event which takes care notifying the user of some such system failure and then properly closing it down. Crash to desktop cant be completly avoided but most of the crash to desktop events you see in moddern games is a sign of pore architecture, the game should have caught the event, informed you about it and closed out nicely.&#x20;

There are of course other system events that are a bit less dramatic such as Shutdown, Network Lost, etc.

**Should I use Game Events for all my events?**

No

Scope is always important, you dont usually want player killed event to be always available for example an event like that is probably best served on the player object as a deligate or Unity Event. You should consider using Game Event over Unity Event though when you have events or actions that are clearly global or whoes scope either changes during run time or cant be well defined in terms of your game architecture ... for example a player killed event might fit as a Game Event if your game is multi-scene and the player character persists through sessions as it does in some online competative games while traditional RPG or games where the session is self contained the event probably fits better on a MonoBehaviour or similar as a Unity event or deligate.

### What is an Event Anyway?

In its simplest form an event is a pointer to one or more funcitons that should be invoked when the event is "raised" or "invoked" depending on your terminology. In more proper terms (I use proper very loosly here) an event is just a deligate (reference to) and in older approches would have been refered to as a "functor" ... that is a "funciton pointer" ... functor, deligate, UnityEvent and GameEvent arn't the exsact same thing in terms of implamentaiton but in practice they enable the same behaviour ... that is the ability to make some stuff happen when some "event" or otherwise "on demand" in your program.

Event based architectures where all the rage not long ago ... a trend that comes and goes ... feel free to google it you will find far better articles than we have time for here. In all games though you will have at least some events and many of those will be best served as "Game Events" to use Heathen's terminogly that is events that should be global to the instance of the game.

### UnityEvent vs GameEvent

You can really think of them as the same thing just used in different scopes. A UnityEvent is something you add to a MonoBehaviour so its on a GameObject and thus its scope starts when it is initalized and ends when it is destroyed. In contrast a GameEvent is a ScriptableObject and thus its scope starts when your game loads and ends when your game is closed.

Aside from scope they are used in much the same way in terms of `AddListener` and `Invoke` etc. even the ability to make custom and complex event types that take multiple paramiters.

### Event Types

Just as you see with UnityEvent\<T> Heathen has created an easy to use base class GameEvent\<T>, but we have taken it a lot further. First you can create your own base GameEvent types using the IGameEvent\<T> and IGameEvent interfaces. Second we pre-created events for the common types to save you from write so much boiler plate code.

{% hint style="info" %}
All Game Events carry EventData as its paramiter, event data holds information such as the caller of the event as well as any data passed into the event. For example the handler for a StringGameEvent might look like this

```csharp
public void HandleStringGameEvent(object sender, string data)
{
    ...
}
```
{% endhint %}

You can find the following types already created for you

* Bool Game Event
* Collider Game Event
* Collision Game Event
* Double Game Event
* Float Game Event
* Int Game Event
* Long Game Event
* Scene Process State Game Event
* String Game Event
* Unsigned Int Game Event
* Unsigned Long Game Event

We then keep going and creatd the concept of "Change" events which handle the concept of the data being changed from an old value to a new value making it very useful for driving system setting events such as volume change, display settings change, etc. and as we did with basic GameEvents we created common use Change Events for you including

* Bool Change Event
* Double Change Event
* Float Change Event
* Int Change Event
* Long Change Event
* String Change Event
* Unsigned Int Change Event
* Unsigned Long Change Event

Finally we insured it was simple to create custom GameEvents, ChangeEvents and CollectionChangeEvents ... change events that drive on collection change. You will find base and template classes for each

* GameEvent
* GameEvent\<T>
* ChangeEvent\<T>
* CollectionChangeEvent\<T>

## Configuration

Creating a new GameEvent or any type derived from it is a simple matter of creating  the scriptable object via **Create > System Core > Events** and then select the desired event type.

To expose a GameEvent to the inspector such that you can connect MonoBehaviours to it use the corasponing Game Event Listener ... you will find there is one for each type.

![](<../../.gitbook/assets/image (136).png>)

This lets you connect behaviours up to the event just like you would a regular Unity Event.

You can also invoke events via the inspector if you so choose such as through a button click

![](<../../.gitbook/assets/image (137).png>)

## Code Examples

### Reference a GameEvent

In all the code examples you will need  reference to the GameEvent and the most common way to do that is to simply drag and drop it from the inspector into a field on your behaviour.

```csharp
public class MyBehaviour : MonoBehaivour
{
    ...
    
    public GameEvent gameEvent;
    
    ...
}
```

Once you have a reference to your event you can work with it as you would any other event

### Add Listener

You can add a listener to the event just as you would to a UnityEvent e.g.

```csharp
gameEvent.AddListener(HandleGameEventInvoked);
```

### Remove Listener

Removing a listener also works the same as a Unity Event e.g.

```csharp
gameEvent.RemoveListener(HandleGameEventInvoked);
```

### Invoking an event

You can invoke an event just as you would a Unity Event e.g.

```csharp
gameEvent.Invoke();
```
