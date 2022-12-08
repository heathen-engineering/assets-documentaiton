---
description: >-
  Understanding the concepts of a callback and other delegates as it relates to
  C# and Unity
---

# ☎ Callbacks & Delegates

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This article will touch on the concepts of a callback as it relates to programming in C# for Unity. This article is not intended to be a primary teaching source, rather an exploration of the feature as it relates to typical approaches you might see in Unity scripts.&#x20;

{% embed url="https://www.youtube.com/watch?v=U-B1PkIS_ug" %}

## Learning First

While there are many "code free" tools to help prototype, and many would claim fully create a game with no programming required, you and your users will benefit greatly from a basic level of programming skill.  In particular this will be important to achieve a level of quality in terms of your user experience in particular around the use of callbacks, delegates and event driven architectures.

Learning the basics shouldn't be scary at all, and in our opinion can often be done faster and to a higher degree of mastery easier; than the effort involved in learning many of the "Visual Programming" tools. At the end of the day you probably already know how to type, so you already know more about programming than you do about some visual scripting tool since creating code is just literally typing words.

{% embed url="https://learn.unity.com/pathway/junior-programmer" %}

Unity Learn is a site provided by Unity that helps teach various skills around Unity game development, and the [Junior Programmer](https://learn.unity.com/pathway/junior-programmer) path is a great starting place for absolutely anyone who will be using Unity at all.

## Understanding

If you want a more primary source of learning around the concept, please review sources such as Microsoft's documentation on the subject

{% embed url="https://docs.microsoft.com/en-us/dotnet/api/system.action-1?view=net-5.0" %}

In short a "delegate" is just a pointer to a method. There are a few ways to accomplish this but the most commonly seen in Unity are the UnityEvent class, and Action class. UnityEvent is used for creating "events" that can be seen and used through the Unity Inspector while Action is a simple delegate tool from C#'s System library that lets us pass in methods as parameters on methods.

For our purposes the term `callback` refers to any pattern where in calling some function causes a "callback" to a desired function. This will typically mean the use of Action but could be accomplished through other mechanisms.

Example

```csharp
public void Foo1()
{
    Debug.Log("Foo1 processing, calling Foo2");
    Foo2(Foo3);
}

public void Foo2(Action callback)
{
    Debug.Log("Foo2 processing, invoking callback");
    callback?.Invoke();
}

public void Foo3()
{
    Debug.Log("Foo3 processing");
}
```

The above code would result in output such as:

```
Foo1 processing, calling Foo2
Foo2 processing, invoking callback
Foo3 processing
```

{% hint style="info" %}
Notice in the above code how we call the callback

```csharp
callback?.Invoke();
```

The question mark there (?) tells the compiler to check for null, if null return null, else call Invoke(); this is the same as writing

```csharp
if(callback != null)
    callback();
```
{% endhint %}

Methods that take callbacks as parameters can be called using [Lambda Expression. See our article on Lambda Expression as it applies to callbacks here.](lambda-expressions.md#callbacks)

## Callback Examples

Callbacks are typically used with asynchronous calls, such as calls to web services, other processes or multi-threaded calls. A callback operates much like an event however a callback is for that purpose only where as event is registered to aka "listened to" and may be invoke by any range of processes where a callback is passed into the call that will ultimately invoke it and at the end of that call is "out of scope".

### Coroutine Example

```csharp
public IEnumerator DoPsedoAsyncWorkInUnity(Action callback)
{
    yield return new WaitForEndOfFrame();
    
    callback?.Invoke();
}
```

This example would be used with Unity's concept of a coroutine where you would pass in a function to be called when the process completed.

Calling this might look like

```csharp
StartCoroutine(DoPsedoAsyncWorkInUnity(HandleWorkDone));
```

Where HandleWorkDone is some function in your code.

### Passing Parameters

Callbacks can take up to 16 parameters, for example

```csharp
public void Foo(Action<string, int, float> callback)
{
    callback?.Invoke("Hello World", 42, 6.9f);
}
```

## Event Examples

Events are not as often referred to as "callbacks" because they are not typically passed in as an argument on a method call for "callback".

That said the term callback gets quite muddy and you will see uses such as in Steam API where "callback" really means an event.

What makes the difference is that an "event" is something raised in response to some condition. Said event may have 0 to many "listeners" that is there may be none or many delegates registered to that event.

Some typical examples of events might include

**MouseOver** event as seen on many uGUI objects

or

**Click** event as seen on the uGUI Button for example

The point is the event is more akin to an announcement that said "event" has occurred

In contrast to events callback usually refers to a delegate passed into a method as a parameter so that said method can "callback" when required. So where an event is more of an announcement a callback is more like asking your friend to hand you the keys ... your friend wouldn't stand up on the chair and yell out ... I HAVE THE KEYS ... as if the event KeysFound was raised ... nope they would simply hand you specifically the keys.

### UnityEvent

You can add an event to a game object such as&#x20;

```csharp
public class ExampleClass : MonoBehaviour
{
    public UnityEvent someEvent;
}
```

This would cause "Some Event" to appear on the inspector window for this object and would let you drag in a method that took no arguments.

In contrast if you wanted arguments you could declare a custom event such as

```csharp
[Serializable]
public class CustomStringEvent : UnityEvent<string>
{}
```

Notice we don't need to write any code here, we just need to declare the class and make it serializable so the inspector window can draw it.

```csharp
public class ExampleClass : MonoBehaviour
{
    public CustomStringEvent someEvent;
}
```

Now the inspector will show Some Event on the inspector and it can take methods that have a string parameter as the argument.

### GameEvent

Heathen created the concept of a Game Event that is a way to declare an event as part of the project as opposed to just a part of some class. You can read more about [Game Events here](../../../assets/system-core/game-events.md).

{% embed url="https://kb.heathenengineering.com/assets/system-core/game-events" %}

### C# event

Event its self is a keyword in C# and it means a collection of delegates. This works a lot like a Unity Event only it wont show up in the Unity Inspector.

As Unity developer we do suggest you use UnityEvent if only for the maintainability of it. That is since the rest of the Unity echo system uses it you should to as being different for the joy of it makes life harder for you and everyone else.

But if you just want to see the world burn you can learn more about C# events here.

{% embed url="https://docs.microsoft.com/en-us/dotnet/standard/events/" %}
