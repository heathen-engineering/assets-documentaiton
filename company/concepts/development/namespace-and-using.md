# 📑 Namespace and Using

<figure><img src="../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

Namespaces are a critically important concept that sadly is ignored by so many Unity developers including Unity its self from time to time. This article will help you understanding what a namespace is and why its absolutely critical that you always define your code within a namespace. The proper use of namespace is important not only for your own good, but also for anyone that will use your code or who will author code that you use.

{% hint style="danger" %}
There is never an occasion that you can forgo using a namespace
{% endhint %}

## ALWAYS USE A NAMESPACE

{% hint style="danger" %}
Without exception always define all of your code in a properly formed namespace
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=LtQs5FzdQ2k" %}

One major issue with learning to program through Unity, is that Unity is absolutely horrible with how it handles its coding style in particular around common conventions like namespace.

{% embed url="https://learn.unity.com/tutorial/namespaces" %}

Strangely Unity considers the use of namespaces as an "intermediate" concept, and only references it as import for code organization. However, this couldn't be further from the truth. Properly formed code is more than just about organizing your class objects, it helps reduce the risk of ambiguity which can result in bugs that don't through errors and can be incredibly difficult to track down even for a skilled engineer.

This topic bares more attention than we will give it here, so just accept that **ALWAYS** using a namespace in **ALL** of your code is an absolute must.

### Why?

The main need in the context of game development is disambiguation (to make something non-ambiguous).

So for example if you created a class such as:

```csharp
public class Input
{
    //...
}
```

You can clearly see why this would be bad if you don't use a namespace, since this will be ambiguous with UnityEngine.Input in any MonoBehaviour&#x20;

```csharp
using UnityEngine;

public class MyClass : MonoBehaviour
{
    public void Foo()
    {
        Input //This is your custom input not UnityEngine.Input
    }
}
```

{% hint style="danger" %}
Ambiguity such as what is shown here is a common cause of errors. Less so with something such as Input but more so with commonly used names such as Player, Character, CameraController, Item, etc.



Someone makes a class with that name, doesn't put it in a namespace and has now broken every case that did use a proper namespace because the compiler will resolve to the object in the global namespace first.
{% endhint %}

{% hint style="info" %}
You may be thinking 'well just name it unique'



That is exactly what a namespace does, but in a way more useful than just really long or cryptic/decorated object names.



namespaces are used by the IDE and compiler for context, driving autocomplete and other features that guide and speed up your development and reduce logical errors. Namespaces have additional features such as aliasing which given even greater flexibility to the developer using them when compared to long or decorated naming.
{% endhint %}

Countless others have said it better; just google "Why should I use a namespace" maybe add "in C#" or "in Unity" if you want to narrow those results.

{% embed url="https://www.geeksforgeeks.org/c-sharp-namespaces" %}

{% embed url="https://stackoverflow.com/questions/5915033/use-of-namespaces-in-c-sharp" %}

{% embed url="https://en.wikibooks.org/wiki/C_Sharp_Programming/Namespaces" %}

## Using

Understanding the using directive and statement can save you a lot of time and headache.

{% embed url="https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-directive" %}

### Aliasing

Lets take a look at a common use case for alias use.

```csharp
HeathenEngineering.SteamworksIntegration.API.Input
```

That is the fully qualified name of a static class in the Steam API. Lets assume your not using aliases.

```csharp
using UnityEngine;
using HeathenEngineering.SteamworksIntegraiton.API;
```

Can you see the issue we are going to have?

The compiler knows both namespaces contain a class `Input` so if you try to call Input the compiler will throw an error and ask you to fully qualify the name, which is a really long name in the case of Steam API :joy:

```csharp
//For the Steam API one
HeathenEngineering.SteamworksIntegration.API.Input;

//For the UnitEngine one
UnityEngine.Input;
```

Now the better way: Aliasing the namespace

```csharp
using Unity = UnityEngine;
using API = HeathenEngineering.SteamworksIntegration.API;
```

Now you can qualify the names with a much shorter token

```csharp
//For the Steam API one
API.Input;

//For the UnityEngine one
Unity.Input;
```



But wait, there's more

Did you know you can use a static class like a namespace and even alias it?

You should if you read the article I linked above, but here is an example. In the Steam API all the static classes such as Input have at least 1 sub class, this is because the API differs for Server and Client. So to do something you might call:

```csharp
Input.Client.GetControllers;
//or
Input.Client.GetAction(...);
```

You can see we have to call the subclass Client every time and that is a bit annoying, so we could  use the Input.Client as a namespace and alias it

```csharp
using SteamInput = HeathenEngineering.SteamworksIntegration.API.Input.Client;
```

So now we can say

```csharp
SteamInput.GetControllers;
//or
SteamInput.GetAction(...);
```

{% hint style="info" %}
Why not just name it SteamInput to begin with?



SteamInput wouldn't be unique in every game, us using a long namespace with nested static classes insures the name is absolutely unique and there is no ambiguity.



You can then decide what you want to call it in short hand for your script, and it can have a different alias in every script if that suits your needs. using this model we give you the flexibility. If we didn't use a namespace or used a flat namespace with decorated names, you would have to take what we give you; which may well collide with other tools your using.
{% endhint %}
