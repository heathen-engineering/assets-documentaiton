---
description: Discover the features and capabilities of Heathen's Steam API objects
---

# 📦 Objects

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

The following articles explain in detail the features and capabilities of every object in the Heathen Steamworks integration. In most cases you won't need to read these articles as we have provided full comments in code thus intelliSense and auto-complete in your IDE of course should provide you with much of the same information you will find here.

### Types

Heathen's Steamworks is built for Unity and so exploits design paradigms common to the Unity development experience.

#### Components

A component is a C# class that is derived from Unity's MonoBehaviour. components can be added to GameObjects in the Unity editor and are generally used to provide functionality to game objects such as UI elements or to act as an interface point between game objects and underlying systems such as the Overlay Manager.

#### Scriptable Objects

A scriptable object is a C# class that is derived from Unity's ScriptableObject. Scriptable Objects or SOs can be instantiated as part of your assets. That is they are created typically at development time and are offten used to store configuration information such as your SteamSettings object.

#### Classes

Never underestimate the power and flexibility of a classic class 😁the majority of Heathen's steam integration functionality is implemented  using class. You will most often be interacting with our static classes located in the API name space such as API.User and API.Overlay.

#### Structures

Structures are the backbone of Heathen's data model. Unlike classes they handled as "value types". They are compact and efficient and while they may have some functionality any such functionality is specific to that instance of that object. For example you can use the UserData structure to get the name of the user the [UserData ](../data-layer/user-data.md)represents.

### Value vs Reference

It is very important to understand the effect of working with classes vs structures. A structure is a value type and will be colored differently by your IDE from reference types such as class objects. When you assign a value type to a variable you are copying its data, in contrast when you assign a reference type you are really creating a pointer to it not copying it ... consider the following.

Lets look at a type Clan defined as follows

```csharp
public struct Clan
{
   public int id;
}
```

Now consider the following operations and there results

```csharp
Clan thisClan = new Clan();    //The value of thisClan.id = 0

thisClan.id = 42               //The value of thisClan.id = 42

Clan otherClan = thisClan;     //The value of otherClan.id = 42
                               //The value of thisClan.id = 42

otherClan.id = 84;             //The value of otherClan.id = 84
                               //The value of thisClan.id = 42
```

Now lets contrast against a class defined as such

```csharp
public class Clan
{
    public int id;
}
```

Now consider the following operations and there results

```csharp
Clan thisClan = new Clan();    //The value of thisClan.id = 0

thisClan.id = 42               //The value of thisClan.id = 42

Clan otherClan = thisClan;     //The value of otherClan.id = 42
                               //The value of thisClan.id = 42

otherClan.id = 84;             //The value of otherClan.id = 84
                               //The value of thisClan.id = 84
```

Notice that when we set the value of otherClan.id that it modified the value of thisClan.id as well ... but why?

The reason is that the variables thisClan and otherClan when the data type is a reference type are really pointers to a location in memory. So in the class based example we only ever called `new` once when we populated the thisClan variable. Thus there is only 1 clan we simply have 2 pointers pointing to it.

In contrast the variables thisClan and otherClan when the data type is a value type are standalone points in memory of that data type. That is when we assigned thisClan to the otherClan variable i.e. `Clan otherClan = thisClan` what we where doing was copying the data from thisClan and writing it into a new point in memory. When we later edited that second point in memory it had no impact at all on the first. Put more simply the value type example using structures created 2 points in memory of type Clan while the class example created 1 point in memory of type Clan.

So why does this matter?

The most common issue Unity developers will run into is operating on value types in a list or other collection. For example a collection of Clan as shown above... Consider the following.

```csharp
foreach(var clan in someListOfClans)
{
    clan.id = 42;    //Invalid for structures valid for classes
}
```

If someListOfClans is a collection public struct Clan then you will get a compiler error. This code cannot be compiled because you cannot modify the member of clan in this manner. If the list is of a reference type then the code will compile and will act to set every clan's id to 42.

so how do you set the values? the same way you would if it was a list of ints or floats or any other value type

```csharp
for(int i = 0; i < someListOfClans.Count; i++)
{
    var clan = someListOfClans[i];
    clan.id = 42;
    someListOfClans[i] = clan;
}
```

In short we copy the memory to a point we can work on it, we edit the memory and we assign it back to the collection at the same offset. Its more steps yes but is also more efficent over all considering the typical use of these primatives.&#x20;

Heathen has take care of when and where it uses this value type vs reference type such that you should rarely if ever need to do anything like this. In objects that we know you will iterate over and be passing around through other objects for modification we have made them reference types such as componenets, scriptable objects and class objects. For all primative types which need to be compact and efficent we use value types.
