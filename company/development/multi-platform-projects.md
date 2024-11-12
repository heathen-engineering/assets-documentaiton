---
description: Parallel development vs single code base
---

# 🤹‍♀️ Multi Platform Projects

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../where-to-buy/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This article will go over the considerations, problems and available solutions when building for multi-platform.

{% hint style="warning" %}
No it is not possible to truly have 1 code base for all platforms.\
\
While many would like to say it is, what they are really referring to is conditional compilation where in compiler adds or removes code from the build based on script defines / build target. We will have more on [conditional compilation](conditional-compilation.md) soon.\
\
This however means that in Unity Editor the code is very different from what will be compiled causing many issues in development and testing.
{% endhint %}

## Considerations

### Platform

Platforms would be things like Steam, Epic Store, Game Pass, etc. but also XBox, PlayStation, Switch, and so on. Your platform is not the same as your build target. Many "platforms" exist on a single build target in the case of PC/Mac and Linux. Platforms however do have specific requirements in order to deploy on them, usually in the form of some API or service that your game must integrate with. This in and of its self means that a "multi-platform" game \***must**\* have unique code bases for each platform.

You may think "Ah sure I can have a define for each platform" ... but this would cause issues for you. If you use defines for conditional compilation in editor then in editor objects will come and go. Take for example Steam, you can "disable" Steam API compilation via the DISABLESTEAMWORKS define. If you do that in editor however it will mean that all of the Steam objects go away and the next time Unity saves it will save without them meaning all the data they held such as configuration, settings, etc. will be gone.

### Built Target

Most "platforms" also have a single dedicated build target e.g. XBox, PlayStation, Android, etc. so for these cases changing the build target also conditionally removes related code. Lets look at Steam as an example again.

Because Steamworks.NET simply will not compile or be available at all in editor or otherwise for any built target other than the three listed

* Mac (client or server)
* Linux (client or server)
* Windows 32 or 64 bit (client or server)

Then switching your project to any built target other than those will result in compiler errors.

&#x20;... however you should never do this in the Editor.

Because if you do this in Editor Unity will not compile any of the Steam related scripts thus any use of those scripts in a scene or GameObject will be removed the next time Unity saves thus breaking all references to all Steam related scripts and objects.

That is if you for example set your editor to `Android` then Unity will see that those scripts no longer exist, it will then remove them from the GameObject on the next save which happens on each platform change.

### Unit Testing

This is what we usually call that testing that a programmer does as they are writing code. Its not a "real" test in that its not a full functional test it does though help the programmer confirm their logic and is an important part of programming.

Doing this in a multi-platform project is tricky ...&#x20;

1. In a project with multiple build targets the programmer will most likely want to switch the editor to the build target for testing. This will cause issues as noted in the [Build Target](multi-platform-projects.md#built-target) section.
2. In a multi-platform project on a single build target such as Steam vs Epic vs Itch, etc. the programmer will want to test with platform specific bits in and again out for each supported platform. Again in editor this will cause the issues noted in the [Platform ](multi-platform-projects.md#platforms)section.

## Solution: Parallel Development

{% hint style="success" %}
This is an ideal solution but only works if you have strong software engineering rigor and solid ALM and DevOps tooling. Beyond that this method really only offers a net gain in cost when you have a large enough engineering team to really exploit its benefits.
{% endhint %}

This is a Application Lifecycle Management (ALM) concept specifically a Development Operations (DevOps) concept. This is a more advanced topic that requires a degree of software engineering rigor not common in most game development teams indie or otherwise. What we mean by "Parallel Development" is that we have multiple parallel branches or "versions" of some code base being developed in parallel that is at the same time.

This works well for multi-platform in that each platform can be a branch of a common code base. This in turn means that common changes performed in the parent branch can be integrated easily into the platform branches. Depending on your DevOps tooling you may also be able to reverse integrate common changes from platform branches up to your common code base for later integration into all platforms.

## Solution: Build Service

{% hint style="success" %}
This is the simplest option and works well for simple projects ... that is projects that have very little platform specific code or configuration. This is really only of value in projects that are small or have a common platform as well since you cannot perform unit testing in editor for each platform.
{% endhint %}

For this you will need to keep your Editor always set to your more common build target typically for mid to high end game projects including mobile builds that will be:

* Mac (client or server)
* Linux (client or server)
* Windows 32 or 64 (client or server)

For projects that have a browser build use&#x20;

* Web GL

This is to insure that the Unity Editor does not strip out any of the code that you need to work with and does not break references to any of the objects you need to work with.

In order to test other platforms you will need to use a build service to build your game for each specific platform where that "build target" will be configured to enable and disable various blocks of code at compile time via the use of Script Defines or similar.

### Unit Testing

Unit testing ... that is the testing done by your programmers in editor; is a bit more of a challenge when your depending on your build service to handle multi-platform builds. This is because your "editor" version of the code base is the most inclusive code base and thus very different from any given build which will be stripped down to have less than the editor.

How exactly you get around this limitation will depend more on your team and your project more so than any given "best practice". Follows are some options you might consider.

#### Sandbox

You or rather your programmers will probably have this anyway ... some times called a "test rig" or similar. This is just a set of scripts and scenes where programmers can try things out. Thus they can simply write a test method to run their logic regardless of platforms or build targets

```csharp
[ContextMenu("Run Foo 1 test")]
public void Foo(int data)
{
    //This is my non-since test method logic here will just run when I call it
}
```

The issue with this is that its truly in isolation, that is these tests cant really account for how this logic works in System testing and is only useful for Unit testing.

#### Conditional Code

Programmers love to write code for them and often forget to remove it from scripts before it goes off to compile. So it can be handy establish a practice of "editor code"

```csharp
#if UNITY_EDITOR
// This code only happens when running in editor
#endif
```

You can carry this on to be more complex for example

```csharp
#if UNITY_EDITOR
#define SteamPlatform
//#define EpicPlatform
//#define GamePassPlatform
#endif
```

This only runs in editor and lets the programmer set defines that are only useful for them ... for example

```csharp
#if !DISABLESTEAMWORKS || SteamPlatform
//This code compiles on builds that are Steam platforms and in editor if 
//the programmer uncomments the #define SteamPlatform
#endif
```

If your dealing with few platforms you can do this even simpler

```csharp
#if !DISABLESTEAMWORKS || UNITY_EDITOR
//This will always compile in editor but in a build only for Steam
//If you want to disable this just comment out the || UNITY_EDITOR such as
// #if !DISABLESTEAMWORKS //|| UNITY_EDITOR
#endif
```

## Solution: Multi-Project

{% hint style="warning" %}
This model is the most error prone and work intensive option but doesn't require any special tooling or engineering practice rigor.



This is similar to "Parallel Development" in that you end up with multiple code bases. The key difference here is that you have no tool or system that helps you integrate changes between platform versions and you probably do not have a "common" code base anywhere.
{% endhint %}

This is simply having 1 Unity project for each platform target such as&#x20;

* Steam
* Itch
* Mobile
* Console
* etc.

This does mean that making changes to "common" code requires you to make those changes to all your projects. You can simplify this slightly by using Unity's Export asset feature. That is if you organize your project assets and code correctly you could write it one and simply export it for reimport into each of your remaining platforms. In this way you get a sort of "pore mans" parallel development model that doesn't require any special tooling and minimal rigor.
