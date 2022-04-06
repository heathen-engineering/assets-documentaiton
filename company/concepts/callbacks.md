---
description: >-
  Understanding the concepts of a callback as it relates to software engineering
  and programming in C#
---

# Callbacks

## Introduction

This article will touch on the concepts of a callback as it relates to programming in C# for Unity. This article is not intended to be a primary teaching source, rather an exploration of the feature as it relates to typical approaches you might see in Unity scripts.&#x20;

## Learning First

While there are many "code free" tools to help prototype, and many would claim fully create a game with no programming required, you and your users will benefit greatly from a basic level of programming skill.  In particular this will be important to achieve a level of quality in terms of your user experience in particular around the use of callbacks, delegates and event driven architectures.

Learning the basics shouldn't be scary at all, and in our opinion can often be done faster and to a higher degree of mastery easier; than the effort involved in learning many of the "Visual Programming" tools. At the end of the day you probably already know how to type, so you already know more about programming than you do about some visual scripting tool since creating code is just literally typing words.

{% embed url="https://learn.unity.com/pathway/junior-programmer" %}

Unity Learn is a site provided by Unity that helps teach various skills around Unity game development, and the [Junior Programmer](https://learn.unity.com/pathway/junior-programmer) path is a great starting place for absolutely anyone who will be using Unity at all.

## Understanding

If you want a more primary source of learning around the concept, please review sources such as Microsoft's documentation on the subject

{% embed url="https://docs.microsoft.com/en-us/dotnet/api/system.action-1?view=net-5.0" %}

For our purposes the term `callback` refers to any pattern where in calling some function causes a "callback" to a desired function.

Example

```csharp
public void Foo1()
{
    Debug.Log("Foo1 processing, calling Foo2");
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

## Examples

Callbacks are typically used with asynchronous calls, such as calls to web services, other processes or multi-threaded calls. A callback operates much like an event however a callback is for that purpose only where as event is registered to aka "listened to" and may be invoke by any range of processes where a callback is passed into the call that will ultimately invoke it.

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
