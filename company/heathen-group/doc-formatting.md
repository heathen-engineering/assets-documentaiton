---
description: Understanding Heathen documentation formatting.
---

# Doc Formatting

{% hint style="success" %}
This standard is newer than some of our articles so some things may not yet be moved over into this format.&#x20;



If you find something that is missing or confusing let us know we are deeply invested in helping you Do More with Heathen.
{% endhint %}

## Overview

Here we will outline the general format to our documents, how to read them and why we do it this way.&#x20;

{% hint style="info" %}
#### I just want know how to make it work!

If you take the time to understand the basics everything else will come faster and easier. The fastest way to reach your goal is to do it the right way first.
{% endhint %}

## Organization

Heathen has many products most of which are integrations with large complex systems and interfaces. The bulk of what Heathen does is make these mammoth systems Unity friendly thus enabling the designer, artist, programmer, scripter and even the engineer to **Do More** with Heathen.

Thus our documentation is equal to the things we are documenting ... that is mammoth in size. To help make it a bit more browsable and digestible we have developed the following common pattern.

* Product Name\
  The root of the product's documents and typically an introduction into what it is and why it is.
  * Installation\
    How to install the product and occasionally notes on installing 3rd party extras that are related to it.
  * Learning\
    All sorts of learning materials, here you will find documentation on any sample scenes, core concepts about the system and then extended tutorial articles on key subjects.
  * API\
    Most of our assets are layered, including a low level programmer centric tool kit or "API" (Application Program Interface) this section will outline all the features and members of the API layer.
  * Components\
    Most of our assets are layered, including high level designer centric tools or "Components", these can be added to GameObjects and are very Unity Editor focused. This section will out line all the components in the product.
  * Objects\
    Most of our assets have complex data models and we do favour the use of Scriptable Objects over singletons and similar and so here you will find all those objects that are not APIs and not Components. These are typically used by either or both the APIs and the Components.
  * Enums\
    Some systems have a lot of named flags or enums, we split these out here for ease of access.
  * Tools\
    Some systems have additional tools, such as the uGUI Tools for Steamworks. These will be described under the tools section.

## Namespaces

Heathen Engineering uses namespaces; and absolutely everyone that writes any code at all for any reason at all should be using them as well. The following article is dedicated to this topic:

{% embed url="https://kb.heathenengineering.com/company/concepts/namespace-and-using" %}

## Object Definitions

When reading any code documentation such as in the API, Components or Objects sections of our product documents you will see a common format where at the top we describe the name of the object and its namespace; i.e. its "definition".

Such as:

Namespace

```csharp
using AppClient = HeathenEngineering.SteamworksIntegraiton.API.App.Client;
```

Definition

```csharp
public static class App.Client
```



or

Namespace

```csharp
using HeathenEngineering.SteamworksIntegraiton;
```

Definition

```csharp
public class ClanChatDirector : MonoBehaviour;
```



This approach tells you that in order to use this code object in scripts you need to include the using statement as indicated above, and the Definition part tells you quite a few things as listed below.

### Accessibility

{% hint style="info" %}
Accessibility

public, private, protected, internal, protected internal, and private protected\
\
These are features of C# and a matter of general programming, if these concepts are new to you please [consult the following article which details each option](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers).



This aspect tells you how and where this object can be accessed.
{% endhint %}

### Type

{% hint style="info" %}
Type\
class, struct, interface, enum, nullable and tuples\


These are concepts of C# again and a matter of general programming, if these concepts are new to you please [consult the following articles](https://docs.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/types).
{% endhint %}

### Name

This is simply the formal name of the object in question, the full "signature" of the object would be its namespace + its name e.g. `HeathenEngineering.SteamworksIntegration.ClanChatDirector` for example.

### Inheritance & Interfaces

Where applicable we will also outline what this object inherits from, this helps you understand how you can use it in the context of Unity and other objects. For example all Unity Components must inherit from `MonoBehaviour` or from a class that its self is derived from `MonoBehaviour`. similarly many tools operate not on a specific class but on an Interface such as [IUserProfile ](../../assets/steamworks/ugui-tools/interfaces/iuserprofile.md)in the [uGUI Tools for Steam](../../assets/steamworks/ugui-tools/), this means any object that implements (inherits) [IUserProfile ](../../assets/steamworks/ugui-tools/interfaces/iuserprofile.md)can be used with it.

{% hint style="info" %}
Inheritance and Interface implementation is concept of C# and a matter of general programming, if these concepts are new to you please consult the following articles.\
\
[Inheritance](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/object-oriented/inheritance)\
\
[Interfaces](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/interfaces)
{% endhint %}

## Field & Attribute Definitions

{% hint style="info" %}
Using standard naming convention all fields will start with a capital case and all attributes will start with a lower case.

```csharp
public bool Field { get; set; }
public bool attribute;
```


{% endhint %}

This naming convention is Microsoft's standard and the Visual Studio IDE will help you maintain it by suggesting name formatting fixes. Unity however is horrible about mangling syntax standard :) so just because its lower case in Unity doesn't mean its not a field.

Visual Studio can help you identify what is what in its auto complete and suggestions

![](<../../.gitbook/assets/image (167).png>)

Here we see that "example" has a member of type `Attribute` named `attribute` and it has a member of type `Field` named `Field` you can tell not just by the proper syntax formatting (lower case attribute, upper case field) but also by the icon beside them (blue box = attribute) and (Gear = Field)

### Field

When defining fields and attributes its first keenly important that you understand the deference in a field and an attribute some times called a "property".

{% embed url="https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/fields" %}

A field acts like an attribute in that it can be assigned to using the standard assignment operator `=` and can be read from in the same ... assuming it is accessible. The key difference is that a field's `get` and `set` accessors can have different accessibility, meaning a field can be made read only, or write only by virtue of controlling the accessibility of each. Also of use is that the `get` and `set` of a field are actually methods, so these can run some processing and then return the results as opposed to simply read/write an attribute of the object.

The definition format we use for a field is as follows.

**\<FieldName>**

```csharp
public bool FieldName { get; set; }
```

\<Description>

As with object definitions this give you critical information including the accessibility and type of the field. For example this example is a public bool, meaning it can be accessed from anywhere and deals with True/False values.

We indicate this is a field with the `{` and `}` and between these we tell you what accessors are available, In the above example both the `get` and `set` are available to you. if you saw a field described as the below example

```csharp
public bool FieldName { get; }
```

This would indicate that said field only has an accessible `get` accessor … so you can read data from it but you cant write data to it.

#### Tips

{% hint style="info" %}
It is important to know when a member is a Field as opposed to a simple attribute. A field requires additional processing to execute and must process every time its read. As such when using a field multiple times in a frame you should be cashing that fields value.
{% endhint %}

```csharp
private void Update()
{
    var fieldName = myObject.FieldName;
    //Do stuff with field name all you want
}
```

A great example of this is Unity's Time.time, Time.deltaTime, etc., these are actually a fields and it must calculate the value every time it is read …\
That's a lot of time wasted if your reading Time.time multiple times in a frame … save your self and your players pain and just cashed the value at the top of the frame and then use the cashed value all you like.

```csharp
private void Update()
{
    var deltaTime = Time.deltaTime;
    
    //Now use deltaTime all you like
}
```

### Attribute

An attribute is a simple object property providing direct access to the memory by name e.g.

```csharp
public string fieldName;
```

This is simply a string value that you can access via fieldName such as&#x20;

```csharp
myObject.fieldName = "Some Value Goes Here";
```

## Method Definitions

When defining a method we use the same basic concept and show you how we define it in code

```csharp
public void MethodName(int arg0, int[] arg1 = null);
```

This again gives you a clear understanding on where you can access the method, what its proper name is, what paramiters it has, what order they are in, what data type they are.

Where applicable such as with `int[] arg1 = null` you can see when the parameters is optional due to having a default value.

We will also describe each parameter where it is not obvious due to its name and often times even when it is obvious.

![](<../../.gitbook/assets/image (177).png>)

{% hint style="info" %}
Visual Studio Intellisense is your friend!\
\
See in the above screen grab, how it shows me the comment for the method, lists all the parameters, describes each parameter and even offers suggestions as to what data can be read from here that would be valid for this parameter.

\
[Learn More HERE!](https://code.visualstudio.com/docs/editor/intellisense)
{% endhint %}

## Event Definitions

When defining events we use the same approach, that is we show how the event is declared in code and will describe when it is invoked and what its handler should look like.

For example

```csharp
public UnityEvent evtSomeEvent;
```

This means that this object has a standard UnityEvent type event named `evtSomeEvent` below it you should see an example of a handler for this event.

```csharp
public void HandleSomeEvent()
{
    //Do Work
}
```

This is meant to show you what a valid event handler would look like, e.g. what parameters are required and what they mean if any.

![](<../../.gitbook/assets/image (178).png>)

{% hint style="info" %}
Visual Studio Intellisence is your friend!



See in the above screen grab, we have went to add a listener and typed the desired name of our event handler ... that method doesn't exist yet so Visual Studio suggested completion is offering to create the method for us.

This suggestion comes up when I right click on the red line indicating a problem and then click the light bulb to get suggestions.&#x20;



A programmer that knows how to use its tools expends FAR less effort than one that doesn't and gets FAR more done. More reason to focus on learning the right way as opposed to "Just make it work"

\
[Learn More HERE!](https://code.visualstudio.com/docs/editor/intellisense)
{% endhint %}
