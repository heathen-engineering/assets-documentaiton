---
description: The only way to code!
---

# 🤯 IntelliSense

<figure><img src="../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

{% embed url="https://code.visualstudio.com/docs/editor/intellisense" %}

> IntelliSense is a general term for various code editing features including: code completion, parameter info, quick info, and member lists. IntelliSense features are sometimes called by other names such as "code completion", "content assist", and "code hinting."

## Overview

I assume most of you have used a word process like Word before. So you know that when there is an error or simply a warning of some sort you get a red, blue or other coloured line under the offending word or phrase.

Visual Studio and any IDE (Integrated Development Environment) worth using will do the same thing with your code. And just like Word and other word processors if you simply right click on that offending word or phrase it will offer various suggestions for fixing the problem.

{% hint style="success" %}
Most of the code errors I am shown in support can be fixed your self by simply right clicking on the red line and selecting the one and only suggested fix.\
\
Always see if IntelliSense can get you sorted first … its much faster than submitting a support case for a misspelled parameter or field.
{% endhint %}

IntelliSense can do a lot more for you though than simply correct basic coding errors. Its also able to identify missing `using` statements, incorrect name formatting, logic errors such as reference comparisons and even stub out code for you.

{% embed url="https://www.youtube.com/watch?v=Tgfa7mMe2uY" %}
Heathen is not affiliated this is simply a video that might help those who don't want to read
{% endembed %}

## Use Cases

### Delegates, Events and Callbacks

So you where told to register a handler on some event, but how are you supposed to know what parameters that event needs to work?

![](<../../.gitbook/assets/image (190).png>)

Well actually as your typing IntelliSense will tell you what kind

```csharp
UnitEngine.Events.UnityAction<string> call
```

That means its an action that takes a paramiter of type string, but don't worry you don't need to read.

#### Step 1

Type the name you want for the handler even though it doesn't exist yet.

![](<../../.gitbook/assets/image (187).png>)

#### Step 2

Now we have our lovely little red line telling us hay ... this doesn't exist. You can now follow the steps as we have done for every other use case and be presented with several solutions.

![](<../../.gitbook/assets/image (171) (1) (1).png>)

#### Step 3

The top solution will be to create a new private method suitable for this event handler. Which I have done and you can see the results below.

![](<../../.gitbook/assets/image (167) (1).png>)



### Misspelling

If you have ever gotten sample code from me then you know I misspell a lot of things.

![](<../../.gitbook/assets/image (183) (1).png>)

How could you possibly know what it should be ... well aside from being better at spelling than me? Use IntelliSense! + a little bit of reading ... its a lot I know but we can do it!

#### Step 1

Right click \`Initalized\`

![](<../../.gitbook/assets/image (178).png>)

#### Step 2

Click "Quick Actions and Refactorings"

{% hint style="success" %}
**Pro Tip**

You can just click the little light bulb and skip Step 1

![](<../../.gitbook/assets/image (176).png>)
{% endhint %}

![](<../../.gitbook/assets/image (166).png>)

#### Step 3

Select the best option. Notice it gives you 4 options

* Generate property `SteamSettings.Initalized`\
  This will create a new property in SteamSettings named Initalized of type bool ... handy if I was trying to create a new property but nope I just cant spell so I don't want to do this
* Generate field `SteamSettings.Initalized`\
  This will create a new field in SteamSettings named Initalized of type bool ... again handy if I was trying to create a new field but nope I just cant spell so I don't want to do this
* Generate read-only field `SteamSettings.Initalized`\
  Again no, I am not creating a field of any kind
* Change `Initalized` to `Initialized`\
  Yes ... that's it I just forgot to add that second `i` now it will work!

So we want the 4th option, which is to correct my bad spelling

![](<../../.gitbook/assets/image (170) (1).png>)

### Namespaces

So your copy and pasting some sample code form Discord or somewhere else but one of the objects say `SteamSettings` is giving you a red line, its not found. How can you possibly know how to fix this?

![](<../../.gitbook/assets/image (189).png>)

#### Step 1

Right click SteamSettings

![](<../../.gitbook/assets/image (179).png>)

#### Step 2

Click "Quick Actions and Refactorings"

{% hint style="success" %}
**Pro Tip**\
You could have skiped step 1 by simply clicking the light bulb to the left \
![](<../../.gitbook/assets/image (172).png>)
{% endhint %}

![](<../../.gitbook/assets/image (161).png>)

#### Step 3

Click the solution!

Now there may be multiple solutions, mouse over each to see what it will do for you. In 99% of cases the top solution is the best solution.

![](<../../.gitbook/assets/image (177).png>)

Having done so you can see that it has added the namespace I was missing for me and my error is now gone.



![](<../../.gitbook/assets/image (170) (1).png>)

### Parameters

So you where told to call the XXXX method on some object or class, but it requires parameters how are you supposed to know what they are and what they mean?

![](<../../.gitbook/assets/image (169) (1).png>)

IntelliSense actually tells you what they are and what they mean as you start typing. See in the screen shot above it has listed all the parameters showing there data type. As I go to enter each one it will show me the code documentation for each parameter.

#### Param 1

For the first paramiter I can see its of type `Steamworks.ELobbyType` and given the coloring I can see that is an enum.

In fact as I type the opening pram bracket It highlights the enum for me

![](<../../.gitbook/assets/image (168) (1).png>)

So I can simply press "Tab" or "Enter" to accept that suggestion and use that enum. I can also see what  the enum does based on the documentation.\
note in the screen shot

> type: The type and visibility of this lobby. This can be changed later via SetLobbyType.

So I know what this param does.

#### Param 2 and beyond

So when I am done with param 1 I press `,` as you do in C# to move on to the next paramiter and IntelliSense will show me the code documentation and provide suggestions for the next parameter

![](<../../.gitbook/assets/image (154).png>)

Here its saying

> maxMembers: The maximum number of players that can join this lobby. This can not be above 250

So I know I can type a number here, and the suggestions it will feed me will be any numbers or objects that contain numbers that might fit here.

### Properties

So you where told there is a field or something in XXXX that should help ... the person helping you didn't know the name just that it was there ... so can you use that to help your self?

Yes of course you can, IntelliSense will show you all the members of an object, what they are and what the code documentation says about them.

Lets say you where told that you can find a list of your Achievements on the Steam Settings object but they aren't sure what the list is called.

#### Step 1

Start typing, we know its in SteamSettings so lets start there.

![](<../../.gitbook/assets/image (151) (2).png>)

And the moment we press the `.` as you do in C# to access the properties of an object we are presented with a list of all the members of this object. This list is also smart, so it will take into account the context you are in and what you have recently used and high light that first. I can keep typing if I need to and it will start filtering that list based on the letters I am typing.

In this case Achievements is at the top of the list and I can see from the comment on it

> The list of achievements registered for this application

That its exactly what I was looking for so I am done!
