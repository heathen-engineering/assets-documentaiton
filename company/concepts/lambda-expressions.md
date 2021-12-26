---
description: Understanding the use of anonymous function as it relates to Unity
---

# Lambda Expressions

## Introduction

Lambda expression or often just called "expression" is a way of creating a function (aka a method) in line in your code. This can be exceedingly useful when the body of the function may vary depending on the use such as when creating predicates for searching lists of things or as the callback to asynchronous calls.

## Learning First

While there are many "code free" tools to help prototype, and many would claim fully create a game with no programming required, you and your users will benefit greatly from a basic level of programming skill.  In particular this will be important to achieve a level of quality in terms of your user experience in particular with more advanced but exceedingly useful for game developer's concepts such as lambda expression.

Learning the basics shouldn't be scary at all, and in our opinion can often be done faster and to a higher degree of mastery easier; than the effort involved in learning many of the "Visual Programming" tools. At the end of the day you probably already know how to type, so you already know more about programming than you do about some visual scripting tool since creating code is just literally typing words.

{% embed url="https://learn.unity.com/pathway/junior-programmer" %}

Unity Learn is a site provided by Unity that helps teach various skills around Unity game development, and the [Junior Programmer](https://learn.unity.com/pathway/junior-programmer) path is a great starting place for absolutely anyone who will be using Unity at all.

## Understanding

If you want a more primary source of learning around the concept, please review sources such as Microsoft's documentation on the subject

{% embed url="https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions" %}

Lambda expression is simply a tool for creating an anonymous function.&#x20;

So what does that mean?\
An anonymous function is a function without a signature (doesn't have a name) it a pointer to some instructions but not a named one in a class object or similar. That is the official definition, however its really just a way to write out a body of instructions and assign that body to something. That something can be a delegate as would be the most common use case but it could be anything that is expecting a body of instructions such as:

```csharp
public bool IsLambda => true;
```

The above is exactly the same as writing

```csharp
public bool IsLambda
{
    get
    {
        return true;
    }
}
```

So its just shorthand?\
It can be used that way but no. In the use case above the compiler will apply the instruction on the right side of `=>` to the Get method of the IsLambda member so this is not a true anonymous function since it does end up with a name but it is expression.

{% hint style="info" %}
For note the compiler will assume we are assigning the value to the get in the above case; we can specify where the instructions are assigned if we like e.g.

```csharp
private float target;
public float Target
{
    get => target
    set => target = value;
}
```
{% endhint %}

A more common use case for expression though would be for callbacks and predicates e.g.

{% hint style="info" %}
You can learn more on predicates at the link below
{% endhint %}

{% embed url="https://docs.microsoft.com/en-us/dotnet/api/system.predicate-1?view=net-5.0" %}

```csharp
public List<GameObject> objects = new List<GameObject>();

// Pretend the list is now populated and we want to find the object in the 
// list named OMG so cool!

var target = objects.FirstOrDefault(p => p.name == "OMG so cool!");

if(target != null)
    Debug.Log("Found it!");
else
    Debug.Log("No GO by that name");
```

In the above code the expression

```csharp
p => p.name == "OMG so cool!"
```

Is the same as if we wrote a method in our class such as

```csharp
private bool Predicate(GameObject subject)
{
    return subject.name == "OMG so cool!";
}
```

and used that in our search

```csharp
var target = objects.FirstOrDefault(Predicate);
```

We can also write our expressions to take multiple parameters and operate in a body such as

```csharp
//Assume a funciton such as
public void DoSomething(Action<string, int> callback);
```

We can call that with expression such as

```csharp
DoSomething((p1, p2) =>
{
    Debug.Log(p1 + " and " + p2.ToString());
});
```

**So why note just write the method out like that?**\
Why you would use the expression approach will depend on a few factors mostly when you have a case where data scope is an issue or you have multiple asynchronous calls to account for. Take the following as an example:

{% hint style="info" %}
This is an abstract example meant to be simple to follow, and to paint a picture, it would not be a common thing to do in a game however there are similar more complex cases you would have in a real world project
{% endhint %}

```csharp
public GameObject FindSomeObject(string targetName)
{    
    return objects.FirstOrDefault(p => p.name == targetName);
}
```

Since the predicate delegate only takes 1 parameter being the GameObject its currently testing we cant pass the name in, which means we need to store it some place it can get to it, so if we wanted to do this with a traditional function we might need to do this.

```csharp
private string searchName;
public GameObject FindSomeObject(string targetName)
{
    searchName = targetName;
    return objects.FirstOrDefault(SearchPredicate);
}

public bool SearchPredicate(GameObject subject)
{
    return subject.name == searchName;
}
```

This would work okay for a synchronous search like this however is the process we where running was asynchronous we could no longer use a single global variable to store our search name, we could create a lookup or various other methods of associating a thread with the data in question or we could create an anonymous function for each individual search via lambda expression.

The anonymous function approach is far easier to maintain and doesn't produce any more allocation than many other solutions to this sort of data access problem.

## Don't Go Crazy

Lambda expression is very handy and can be used in loads of places. Its important though to understand that anonymous functions can create more work for the garbage collector if used incorrectly. It is not true to say you should never use expression. Below are some common uses cases and our assessment of the impact both on system performance and maintainability e.g. your ability to keep your code clean and effective.

### Field Members

These are the `get` and `set` you see in C# fields and are perfect use cases for lambda expression with no adverse effects at all as this is not truly an anonymous function its simply a shorter way of expressing the instructions you want to apply there.

```csharp
private bool thisIsAField;
public bool ThisIsAField
{
    get => thisIsAField;
    set => thisIsAField = value;
}
```

Even better when its a get only

```csharp
private bool thisIsAField;
public bool ThisISAField => thisIsAField;
```

### Function Body

This is the literal definition of expression, so a good use case with no adverse effects; but what is it you ask? Take a look at the following, it should shed some light.

```csharp
public List<GameObject> objects;

public GameObject FindObjectByName(string name)
{
    return objects.FirstOrDefault(p => p.name == name);
}
```

You could have written that as

```csharp
public List<GameObject> objects;

public GameObject FindObjectByName(string name) => 
    objects.FirstOrDefault(p => p.name == name);
```

### Predicates

This is nearly always best served as an anonymous function (expression). Predicates typically require data that is not going to be in scope of a fixed/named function and these sorts of searches should already be restricted to as needed thus shouldn't be frequent enough in your system to cause a performance problem.

So what do you do when you do have frequent searches?\
Use a lookup aka an index, if your going be looking up a GameObject by name from some list of GameObjects then index them by name and use a collection control such as Dictionary to more efficiently fetch e.g.&#x20;

```csharp
public Dictionary<string, GameObject> goLookup;
```

Using this you can more efficiently look up a GO assuming

```csharp
// assume we stored the list of GOs we care about such as 
goLookup.Add(GO.name, GO);
```

so then we can get any GO by its name very quickly

```csharp
var target = goLookup["OMG even more cool!"];
```

### Callbacks

Callbacks will very, for asynchronous calls where multiple calls can be made at once an anonymous function (expression) will make your life so much easier and isn't likely to add any more allocation to the system than any other control structure you might use to manage such.

For synchronous calls where the scope of dependent data is not a problem your probably best to define it as a fixed / named function. If scope of data is a problem as it often is with a predicate as noted above then treat it like a predicate and make it anonymous (expression).

```csharp
public void Foo(Action<bool> callback)
{
    //DOWORK
    callback?.Invoke(true);
}
```

In this case we define our delegate as an Action of type bool, this means it expects a function that takes 1 parameter of type bool. you can do this is expression or as a defined method.

```csharp
private void HandleFoo(bool arg0)
{
    if(arg0)
    {
        //DOWORK
    }
}

// ...

Foo(HandleFoo);
```

or

```csharp
Foo((arg0) =>
{
    if(arg0)
    {
        //DOWORK
    }
});
```

### Event Handlers

You will rarely if ever use an anonymous function as an event handler. Event handlers persist for long periods of time and may be called multiple times during the session, they also (generally) are synchronous with no data scope issues so are ideal for fixed / named functions and rather bad use cases for anonymous functions.

### Steam Callbacks

Steam has its own idea's about Callbacks in Steam API a Callback is really an event and so you should treat it like an event. Events are generally never anonymous.

### Steam CallResults

Steam has another concept similar to its Callback, which remember is really an event handler, but a Steam CallResult is more like a .NET Action (aka a callback in our world) or a even a predicate depending on which CallResult your referring to. Steam's CallResults are often good candidates for an anonymous function (expression)
