---
description: System Core Scriptable Variables
---

# Scriptable Variables

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Scriptable Variables allow you to define data points as assets in your project. In short you can define floats, strings, bools or even custom data types (classes or structures) as scriptable objects in your asset folder. This then opens up many possibilities from an architectural point of view.

## Benefits

Unity 2017 had a great talk on this subject and goes deep into the reasons you should avoid the singleton model, and more importantly what the benefits of Scriptable Objects are over singleton and other approaches.

{% embed url="https://www.youtube.com/watch?v=raQ3iHhE_Kk" %}

### Remove Singleton Dependency

The singleton model is a common approach in Unity game development however it is fraught with issues. Singleton dependency that is when one object is dependent on the state of another object’s singleton value (its static attribute) creates hard to trace errors due to null reference exceptions, it creates deep dependency between objects making unit testing difficult or often impossible and can lead to access issues by creating a logical path of reference beyond the scope that would normally be permitted.

Scriptable Variables remove the need for most if not all singletons by storing the data in a mutually accessible location (the Scriptable Variable). Take for example “Player Health” your player character will need to know about this as will your Player UI. You could define the data on Player Character, make that a singleton and have the Player UI use that. Doing that will create a dependency between Player Character and Player UI. It also means that Player UI can now execute methods on Player Character as it has a reference to it, this encourages bad design, creates dependency that means Player UI cannot be tested with out Player Character and means that both Player Character and Player UI must be defined in the same scene or referenced at run time with a costly lookup.

Using Scriptable Variable, you could define Player Health as a variable in your asset database and have both Player Character and Player UI reference that variable. Now neither the character nor the UI is aware of the other. They can be defined in separate scenes and even in multiple scenes. More importantly the Scriptable Variable will report when its data has changed so you don’t need to use an Update loop to react to data change you could choose to use an event-based approach.

### Reduce Data Duplication

Another common issue in game data models is the duplication of data; that is we often see common values such as player health, the current state of UI, etc, needing to be calculated multiple times in multiple places or worse yet being stored in multiple places and needing to be synchronized when change occurs.

A common example of this might be player UI colour preference. You could store this value on each UI controller that needs to use it and thus when this value changes you need to go out and update all references to it. Alternatively, you could use a singleton to hold the value, but this then creates a large and wide reaching dependency chain that will make unit testing difficult if not impossible. Finally, you could create a system to look this value up such as to read it from app settings or similar, this however incurs processing overhead for everything that uses it and thus does not scale well at all.

There are other approaches but none as simple, efficient, and robust as simply having all objects that need it reference the same bit of data without creating dependency between disparate systems or requiring run time look up due to multi-scene setups. This is where Scriptable Variables come in. You can define such global or common data points as Scriptable Variables and reference them cross scene, respond to change events and ensure that there is no duplication of this data and that all users of the data are aware of the latest value all the time.

### Cross Scene Referencing

Can be easily referenced cross scene resolving a common problem with multi-scene game structures. In a multi-scene game, one often runs into the issue that Unity’s editor cannot resolve references between scenes that is you cannot reference an object in Scene A from Scene B at dev time. This limitation is not applied to Scriptable Objects because they are defined in the Asset Database and are thus always “in scope”.

### Always Available

Can always be accessed, unlike a singleton game object structure there is no need to wait for initialization with a Scriptable Variable. The reference is available from the moment the game is loaded into memory. This is contrast to the singleton model; in a singleton model you create a static variable on your game object that gets set on Start of that object which means the period of time between initialization of the game and the start of that object the variable is null.

### Change Event

Heathen Engineering’s take on Scriptable Variable is to derive them from GameEvent\<T> this means that every Scriptable Variable is also a change event for the same type of data. As a result of this design you can receive change notification for any data type whos change is applied through the data field of the variable e.g.

This means for example you could drive the change of a player health bar by change event as opposed to updating every frame saving processing time.

{% hint style="warning" %}
You can create complex Scriptable Variables which represent reference types of data vs value types of data. As such you must be aware that the change event can only trigger if it can detect a change in data e.g. when you set the value via the Variable.Value field or via the Varaible.SetValue(value) method.
{% endhint %}

### Seemless Editor Integration

Heathen's approach to Scriptable Variable referencing means your designers can choose rather they use a reference to a Scriptable Variable enter a constant value in the inspector. By using the FloatReference data type we can let the designer choose if they use a Scriptable Varaible or if they use a constant value.

Take the example below. `oldWay` is a float attribute and can only be typed in as a constant value in the inspector. `betterWay` is a FloatReference and so the designer can choose to type in a constant value or can change the mode to variable and reference a Scriptable Variable of type Float.

```csharp
public class Example : MonoBehaviour
{
    public float oldWay;
    public FloatReference betterWay;
}
```

Using the menu button to the left of the input field the designer can change the mode of Better Way

![Better Way is set to Constant](<../../.gitbook/assets/image (42).png>)

![Better Way is set to Variable](<../../.gitbook/assets/image (45).png>)

## Custom Variables

Heathen's System Core is designed to be extended, you can easily create custom variable types. The standard System Core comes with common data types already defined e.g. float, int, double, vectors of various types and more. You can however create your own including composite variable types - That is types that store complex data not just single values.

Lets assume we have a complex data model such as

```csharp
[Serializable]
public class ExampleCompositData
{
    [Serializable]
    public class MoreComplexData
    {
        public float anotherFloat;
        public bool someBool;
    }

    public float someFloat;
    public string someString;
    public int someInt;
    public MoreComplexData moreData;
}
```

If so then we can define a Scriptable Variable that handles this data type as

```csharp
[CreateAssetMenu(menuName = "System Core/Variables/Custom/Example Composit Data")]
public class ExampleCompositDataVaraible : DataVariable<ExampleCompositData>
{ }
```

Note that we don't need to populate the body of this class, the base class `DataVariable<T>` handles all the logic needed. We do however need to give it a unique `CreateAssetMenu` name so that we can create it from the `Create` menu in the Unity Editor.

Next we need to create the `Reference` this is an optional step, if we want to insist that this data type is always used from a Scriptable Variable and never used as a constant then we can skip this step however if we want to let the designer choose if they type the value in manually in the inspector or if they reference a variable then we need to create a `VariableReference<T>` for the type.

```csharp
[Serializable]
public class ExampleCompositDataReference : VariableReference<ExampleCompositData>
{
    public ExampleCompositDataVaraible Variable;

    public override IDataVariable<ExampleCompositData> m_variable => Variable;

    public ExampleCompositDataReference(ExampleCompositData value) : base(value)
    { }
}
```

Here we are creating the reference type. You can of course use a shorter name 😊 the long name here is just for our example.&#x20;

Once this is done you can create a reference field for this type via&#x20;

```csharp
public class Example : MonoBehaviour
{
    public ExampleCompositDataReference complexData;
}
```

In the inspector that will look like this

![Complex Data is set to Constant mode](<../../.gitbook/assets/image (46).png>)

![Complex Data is set to Variable mode](<../../.gitbook/assets/image (47).png>)

If you wanted to insist that its a variable e.g. not let your designers choose then change the code to use the variable as opposed to the reference

```csharp
public class Example : MonoBehaviour
{
    public ExampleCompositDataVaraible complexData;
}
```

![Variable type, has no menu button](<../../.gitbook/assets/image (48).png>)

Notice that there is no menu button, the designer is thus forced to use a variable of this object.

## Initalize References to a value

```csharp
public FloatReference dataVariable = new FloatReference(42f);
```

Use the `new` keyword to use the default constructor and set the constant value as desired.

## Default Reference to Varaible mode

```csharp
public FloatReference dataVariable = new FloatReference(0f) 
    {
        Mode = VariableReferenceType.Referenced 
    };
```

Using the `new` keyword to construct the value on initialization. You can also set any of the members to any value that can be defined at compile time .e.g you can set the `Mode` to Referenced.

{% hint style="info" %}
Note we are passing in a default constant value in this case as the constructor requires an initialization value. The field will be set to variable mode in the inspector.
{% endhint %}

## Get Varaible Values

```csharp
dataVariable.Value
```

You can access the value of a variable through its `Value` field.

## Set Variable Values

```csharp
dataVariable.Value = value;
```

You can set the value of a variable through its `Value` field. If this value is new it will cause the change event to be raised/invoked.

## Understanding Change Events

All Scriptable Variables are also change events of the same data type; this means you can listen for change of the underlying data assuming of course that data is changed via the Value or SetValue methods.&#x20;

Using the example above as a data type note that the following code will raise the change event

```csharp
complexData.Value = new ExampleCompositData() { ... };

//or

complexData.SetValue(new ExampleCompositData() { ... });
```

And this following code will **not** raise the change event

```csharp
complexData.Value.someFloat = 42f;
```

#### But Why?

Because in the second example the value of the variable's Value attribute did not change, its still pointing to the same object in memory, you simply changed a member of that object's data not the object its self.&#x20;

In the first example we actually set the Value attribute of the variable to a new / different object thus the Value did change and the event gets raised.

#### Raise on member change

If you want to have the change event raise on the change of a member you need to do so manually.

```csharp
complexData.Value.someFloat = 42f;
complexData.Raise(this, complexData.Value)
```

Note you cant simply set the Value to its self, the system does check for equality before raising e.g.&#x20;

```csharp
complexData.Value.someFloat = 42f;
complexData.SetValue(complexData.Value)
```

The above will never cause the change event to raise

## Listening for Change

Variables work like UnityEvents, simply add a listener

```csharp
public void Foo()
{
    complexData.AddListener(HandleChange);
}

private void HandleChange(EventData<ExampleCompositData> data)
{
    //DO WORK
}
```

## Remove Listeners

Variables work like UnityEvents, simply remove the listener

```csharp
public void Foo()
{
    complexData.RemoveListener(HandleChange);
}
```
