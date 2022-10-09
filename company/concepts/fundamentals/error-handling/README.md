---
description: Understanding the importance of error handling
---

# Error Handling

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Error handling refers to the practice of detecting errors in your processes, states and systems, and handling those conditions in a graceful manner. Ideally your game would "recover" from error states but worst case it should report the issue to the user and possibly to your backend services and then gracefully shut down as opposed to the blind crash to desktop.

This section will cover some basic concepts of error handling as they apply to Unity game development, and will highlight areas the UX toolkit can help deliver a better user experience.&#x20;

## Learning First

While there are many "code free" tools to help prototype, and many would claim fully create a game with no programming required, you and your users will benefit greatly from a basic level of programming skill.  In particular this will be important to achieve a level of quality in terms of your user experience in particular around error handling, recovery and reporting.

Learning the basics shouldn't be scary at all, and in our opinion can often be done faster and to a higher degree of mastery easier; than the effort involved in learning many of the "[Visual Programming](../visual-scripting.md)" tools. At the end of the day you probably already know how to type, so you already know more about programming than you do about some [visual scripting tool](../visual-scripting.md) since creating code is just literally typing words.

{% embed url="https://learn.unity.com/pathway/junior-programmer" %}

Unity Learn is a site provided by Unity that helps teach various skills around Unity game development, and the [Junior Programmer](https://learn.unity.com/pathway/junior-programmer) path is a great starting place for absolutely anyone who will be using Unity at all.

## Getting Started

Properly handling errors in your app or game requires you to create a few things.

{% hint style="info" %}
our [UX Complete](../../../../assets/ux/learning/core-concepts/feedback-tools.md) asset can help you with all of these concepts
{% endhint %}

### Dialog

No matter what method of error handling you chose to go with you do need some reliable means to report the errors to the user. This is a the minimal requirement for any kind of error handling solutions. The Error Dialog sub-article goes over this concept in more detail.

### Reporting

This is how you will learn about errors, will you depend on your user's to tell you, how will you gather system information for them so they can provide you with meaningful data. Would it make more since for you to use a Reporting and Analytics service ... hint (yes use a service)

## Tips&#x20;

Once your a few hours into Unity's Junior Programmer course, or if your already quite comfortable with scripting in Unity, check out these quick programming tips; they will help you a ton when thinking about error handling.

### ALWAYS use a namespace

{% hint style="danger" %}
Without exception always define all of your code in a properly formed namespace
{% endhint %}

We have a [whole article on this topic](../namespace-and-using.md) which you can find at this [link](../namespace-and-using.md).

{% embed url="https://kb.heathenengineering.com/company/concepts/fundamentals/namespace-and-using" %}

### What can go wrong, will go wrong

This is a very true statement with any software, or anything really but especially software. If you have some logic that can break, it will break so handle that. C# gives you various tools and one of the easiest to use is the try catch block

```csharp
try
{
    //Some code that could thrown an exception
}
catch(ExceptionType ex)
{
    //What to do when it does throw an exception
}
```

{% embed url="https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/try-catch" %}

You can find numerous video tutorials on YouTube, many of which dealing specifically with Unity and try/catch error handling.

### Dev Time is better than Run Time

If it can be done at dev time, it is better than doing it at run time. This means if you can do it as a configuration that is saved at development time in the editor, as opposed to it being a process that calculates at run time, that is literally more performant in that process at run time consume processor time. Configurations need to be loaded but that is (most likely) always faster than calculating.

Unity's examples very often do something like this

```csharp
public class SomeExample : MonoBehaviour
{
    private MeshRenderer meshRenderer;
    
    void Start()
    {
        meshRenderer = GetComponenet<MeshRenderer>();    
    }
}
```

Just don't. This is a process that happens at run time, you are telling the system to search list of components on this GameObject, and return the first occurrence that is or was derived from the MeshRenderer type. This consumes time and increases the possibility of run time errors.

The better answer is to do this at dev time

```csharp
public class SomeExample : MonoBehaviour
{
    [SerializeField]
    private MeshRenderer meshRenderer;
}
```

Now in the Unity inspector you can drag and drop the desired MeshRenderer into this slot. You know at dev time that it is populated, you know what its populated with and at run time no processing need occur.

So why does Unity's examples show the GetComponenet approach?

We don't know, but assume it's so you don't have the step of dragging and dropping the reference. This means the code example is self contained and doesn't require extra explanation around the use of the inspector. This is just an assumption.

{% hint style="warning" %}
For note using the "transform" member of a mono behaviour is the same as calling GetComponenet\<Transform>() and so takes processing time.

If you will need the transport more than once then reference it e.g.

```csharp
[SerializeField]
private Transform selfTransform;
```

Now you can reference it at dev time and its always available to you

[HeathenBehaviour ](../../../../assets/system-core/heathen-behaviour.md)a tool in System Core does this for you
{% endhint %}
