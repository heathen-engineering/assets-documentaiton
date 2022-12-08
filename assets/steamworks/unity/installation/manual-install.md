# Manual Install

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

If your a GitHub Sponsor you can install Steamworks Complete manually by downloading the source code and simply importing it into your Unity project.

{% hint style="info" %}
Steamworks Complete is dependent on Steamworks.NET and System Core as is noted in the [Prerequisites article](prerequisites.md). If your installing manually so you can avoid needing to fix your Unity Editor's use of Git such as to avoid the "Git Executable Not Found" error ... then know that your still likely to have this issue unless you choose to install everything manually which is likely to create a lot of Human Error issues.
{% endhint %}

## Consideration

This section is a plea for you to reconsider manually installing really anything that can be installed via Unity Package Manager or any other similar managed installation option.&#x20;

### I want to mod the code

No you **REALLY** do not want to modify 3rd party code directly. \
Doing so means

* You cant be properly supported by its author
* You cant be properly supported by the authors of anything that depends on it
* You stand a high chance of breaking it or things dependent on it
* You have nothing to gain that you couldn't gain through other methods

That last point is the main one. You can, without modifying the 3rd party code at all, extend, derive, adapt and implement variation to anything. That is standard and important aspect of languages like C# the ability to modify systems and objects without needing to change there source code.

If you want a prime example of this look no further than our Steamworks asset and Steamworks.NET its self.&#x20;

Steamworks.NET is built on top of Steam API, it does not modify Steam API it extends it and wraps its features and functions up in C# compatible objects. Its not black magic, its not a rebuild of Steam API its simply a .NET wrapper.

Heathen's Steamworks takes that a whole lot further. We are built on top of Steamworks.NET and can even run on top of Facepunch (with limitations). We greatly change how the underlying Steam API wrappers work making it much easier to use and making it compatible with typical Unity game development standards and practices. We do all this without modifying a single line of code of Steamworks.NET (or Facepunch) or the underlying Steam API.

It is always easier and results are better when you use the tools you have at hand in C# to extend, derive, wrap or otherwise change systems and objects without resorting to damaging the underlying source.

### UPM Never Works

Yes it does, what you are expressing is an issue with your environment.

{% embed url="https://kb.heathenengineering.com/company/concepts/fundamentals/package-manager-installs#troubleshooting" %}

We can help you fix your environment, the article above will get you started. \
Here is why you should do it now!

1. Doing it the wrong but fast way is still wrong\
   By avoiding fixing the underlying problems you are just compounding your problems. By not using UPM you are greatly increasing the risk of various issues such as&#x20;
   1. Conflicts in code and merge
   2. Difficulty in update
   3. Significantly higher chance of human error
   4. Lower trust in support (because you cant **know** that your version is 100% right and up to date)
2. Heathen isn't the only one that uses UPM, Unity does as well so fixing your UPM to work with Git URL now will save you time in the future. Odds are you are going to have to use UPM at some point.
3. Error free install and update\
   It is exceedingly easy to mess up a manual install and even easier to mess up a manual update. And you will absolutely be updating your tools during the life of your project. UPM removes the human error component of this and thus makes getting support dirt simple.
4. Dependency Management\
   UPM has a concept of dependency management and can install or update dependencies to meet requirements. This is the main reason asset developers favour it. Its actually more work for us to create packages that are UPM compliant than it is to puke out a standard UnityPackage file. But UPM means we don't have to fight or worry or deal with anywhere near the level of support requests due to bad install and broken dependency.
5. Samples, Tools and Extensions\
   UPM installs have a concept of optional things you can add. This means you can avoid cramming junk into your project like documentation files, sample scenes, etc. unless you really want to.\
   And Samples install into your Asset folder meaning yes you can modify them without any issue.
6. Less Bloat\
   UPM stores the bits you should **ABOSLUTLY** never modify in a protected "packages" folder. This gets all that code and config that you shouldn't be changing out of your Asset folder leaving your Asset folder to be just the bits your working on and thus **MUCH** cleaner.

## I insist on manual

So be it, you will have issues if not now then later owing to this decision but here are the basic steps. Keep in mind when you come to us for support we are going to need you to be on the latest version and we are going to need you to be on an unmodified version of our source if you want us to support it.&#x20;

We obviously cannot support your custom code.

### Download

As a GitHub Sponsor you can download our full "Source Repo" including all of our code for all our major assets. The easiest and recommended way to download the code is to use [GitHub Desktop](https://desktop.github.com/) and "clone" the repository to your disk.

{% hint style="info" %}
You really should clone the repo not simply download the zip

This will save you MUCH pain later.
{% endhint %}

This is recommended as it will make it easy to "fetch" updates as they occur and keeps things organized as we organize them in the repo.

### Copy & Paste

Copy the desired code into your Unity Project.&#x20;

{% hint style="danger" %}
**YOU MUST KEEP THE FOLDERS INTACT**

\
Any UPM based asset will be using assembly defines and assembly defines require the folder structure you find them in to work as expected. If you go merging Editor folders, etc. you will have a **VERY BAD** time.
{% endhint %}

#### System Core

`SystemCore/com.heathen.systemcore`

![](<../../../../.gitbook/assets/image (1) (3).png>)

#### Steamworks.NET

{% hint style="warning" %}
**TO MANUALLY INSTALL STEAMWORKS.NET YOU MUST USE THIS METHOD**\
\
Do NOT use the zip or unitypackage file you find in Steamwork.NET's release folder. that example is (nearly) always out of date and (nearly) always is missing key components such as the assembly define.
{% endhint %}

`Steamworks.NET/com.rlabrecque.steamworks.net/`

![](<../../../../.gitbook/assets/image (6) (1).png>)

#### Steamworks Complete

`SourceRepo/Steamworks/com.heathen.steamworkscomplete/`&#x20;

![](<../../../../.gitbook/assets/image (7) (1).png>)

You will notice 2 subfolders `Samples~` and `Tools~` you should remove the `~` character from the end of there name so that Unity can load them in the editor.&#x20;

![](<../../../../.gitbook/assets/image (1) (2) (1).png>)

If you do not remove the \~ character from the end of the name of these two folders then they will not appear in Unity Editor.
