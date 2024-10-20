# 🔼 Updating Visual Studio and C\#

## Introduction

Unity Installer does a poor job of updating Visual Studio and the .NET Framework so there will be occasions when you need to do this yourself if you work with Unity for any period of time.

Visual Studio and .NET like any bit of software or framework do require the occasional update. If you have ever seen an error such as.

> out variable declaration cannot be used because it is not part of the C# #.# language specification

or&#x20;

> Tuple must contain at least two elements

or

> A new expression requires (),\[] or...

Then the issue you have is you are on an older specification of C# and missing language features.

### More Info

the Tuple issue in particular comes from C#8.0 and older when you try to use C#9.0 and newer features of target-type new declaration.

```csharp
//C# 8.0
MyClass myVar = new MyClass();

//C# 9.0+
MyClass myVar = new();
```

C# 8.0 has no concept of this syntax other than the declaration of a tuple so it assumes the line is attempting to new a tuple but that would require 2 or more parameters hence the error message you see.

{% embed url="https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/new-operator" %}
See the Target-Typed notes for more details
{% endembed %}

{% embed url="https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-9.0/target-typed-new" %}
Link to when this was first announced Nov 2020
{% endembed %}

This is why the advice is to update your IDE to ensure your language definition is current, while its rarely your IDE's fault ... in this case it absolutely is or rather its that your IDE's definitions need an update.

## Visual Studio Installer

The easiest way to update is within Visual Studio itself. In many cases, you will see a yellow banner or flag in the upper right corner of the Visual Studio app you can click it and download and install updates.

If the flag is not present or you prefer another method you can press open the Start Menu on Windows and type Visual Studio Installer

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

In general, we recommend you keep your Visual Studio IDE up to date with the latest option available.

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

It's also advisable to ensure you have all the components of Visual Studio installed for Unity development.

Click the "Modify" option&#x20;

Scroll down to the Gaming section and you will see there are additional tools for Unity

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

It is also strongly advised that you keep the .NET Framework up to date with the latest option. You can expand the .NET Desktop Development option in the right side panel and insure features such as&#x20;

* .NET Framework #.# development tools
* .NET profiling tools
* IntelliSense and or IntelliCode

And similar features are checked for install

## Rider

We don't use Rider so cant speak from experience on how to update it properly
