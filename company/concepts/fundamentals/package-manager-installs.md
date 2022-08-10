# Package Manager Installs

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## What is it

An easy and much more flexible way to install stuff into your Unity Project.

### Why

Its the method used by Unity internally, its the method used to install all Unity open source and community contributions and its the method used by many asset developers … including Heathen.

It has quite a few benefits over the older .unitypackage import method but it does take a bit of learning for users that are new to the concept.

### History

With Unity 2018 Unity started to introduce the concept of the Package Manager.

{% embed url="https://docs.unity3d.com/Manual/upm-ui.html" %}

While in standard Unity fashion the transition away from classic .unitypackage exports to the new Package Manager approach has been

* Slow
* Miss managed
* Clunky
* Painful
* Horrible
* etc. etc. etc.

In classic Unity fashion the benefits have been ... well nothing short of transcending and awe inspiring.

### Yes but WHY

The Package Manager for the first time lets us pull active source ... not a file export ... note a .unitypackage ... that is really just a proprietary zip file ... ya its that bad.

Second we can describe dependencies ... 😍... if your an asset developer creating coded assets this is GOD level awesome.

Finally and one of my favourite features ... no more bloat. Not only can we remove the deep copy of every dependency we might use thus removing the version conflict hell of yester year we can also distribute samples, extensions, demos, etc. as additional downloads. So you no longer need to download 10 gigs of sample content you will never use just to get at the 15mb of code you wanted 🤩💖 ... unless you want to of course ...&#x20;

## Troubleshooting

{% hint style="danger" %}
After you install Git, or if you modify your environment variables, or if any installer, configuration or anything else for that matter might have modified your environment variables … \
\
\*\***Restart your machine**\*\*\
\
Why?\
Unity Hub and various other systems use environment variables to know where things are … sadly many of these don't follow the very most basic of good practices and read these values on demand rather they read once on load and cash the results in there own internal memory meaning they don't get the memo when they change … apparently they think the processing saved from reading from cash is worth the headache this causes when they are working on outdated values.\
\
While full restart is not the only way it is the best, fastest, least error prone way to make sure this issue isn't effecting your … simply fully restart your machine after any change to its environment variables such as installing Git, Visual Studio, updating either or similar software, etc.
{% endhint %}

### No git executable was found

Unity's Package Manager uses git to download and import assets from Git repositories. This is the method used by Unity internally, used for all of Unity's open source and community assets and used by Heathen.

For this to work you must have installed git as per Unity's documentation

{% embed url="https://docs.unity3d.com/Manual/upm-ui-giturl.html" %}

{% hint style="info" %}
Installing Unity Packages via Git URL as we do here requires that you have Git installed. as outlined in [Unity's documentation](https://docs.unity3d.com/Manual/upm-ui-giturl.html).\
\
If you don't have it already you can install Git from the following link:

* [https://git-scm.com/](https://git-scm.com/)&#x20;

Note that this does NOT mean you will be using Git as a source repo, it is simply a set of protocols used by Package Manager to download the required code from its target repository.
{% endhint %}

It is a relativly common problem that Unity isn't able to detect Git once it has been installed. The very first thing you should try is to \*\***restart your machine**\*\*. Sadly Unity doesn't know how to properly read environment variables and so only reads for them once on start up assuming they will never change :joy:

{% hint style="success" %}
If you run into this issue please let Unity know its a problem for you so they can be aware of the frequency of the problem for users and maybe escalate its importance in there queue.
{% endhint %}

Assuming a simple restart doesn't resolve the issue for you the most likely issue is a problem with how the environment variables where set on Git install … or rather where not set.

This YouTube video is not sponsored by Heathen but seems to help a lot of people.

{% embed url="https://www.youtube.com/watch?v=F-8A8mJwL_Y" %}

{% hint style="warning" %}
If you get a message to the effect of \
`No git executable was found`\
\
This video might help you get it resolved

[https://youtu.be/F-8A8mJwL\_Y](https://youtu.be/F-8A8mJwL\_Y)



We are not associated with the creator we have simply been told that video has helped others with that error.



This thread might also be of help for you

[https://forum.unity.com/threads/no-git-executable-was-found-please-install-git-on-your-system-and-restart-unity.730511/](https://forum.unity.com/threads/no-git-executable-was-found-please-install-git-on-your-system-and-restart-unity.730511/)
{% endhint %}

If none of the above works for you then you need to contact Unity's technical support. This is a problem with Unity not with our code and not with anything we can really effect.



To get you going while you wait on Unity's support to get back to you, you can simply download then Git repository for SystemCore or whatever else you need and install it manually.

{% hint style="danger" %}
WE DO NOT RECOMEND YOU DO THIS



Manul instal should be your last resort, it is error prone, can result in Unity making a huge mess when merging assets and generally makes for a bad time.



That said we do enable you to do this and will do our level best to help you with any issues you run into.
{% endhint %}

### I'm a Sponsor but cant install

The most common cause of this problem is that you are not logged into GitHub with the same account that sponsored in such a way that UPM is able to access the private repository where Heathen's assets are stored.

For example

1\) You have multiple GitHub accounts and your Windows Credential Manager is using the "other one" as in the one you didn't sponsor with.

2\) Something else is blocking the popup to login from windows

When you first try to add a package using Unity Package Manager from a private or secured repository you should get a popup that look like this

![](<../../../.gitbook/assets/image (5).png>)

It may not have taken focus so look behind other windows. When you find it click the "Sign in with your browser" button ... that will open your default browser, ask you to login or if your already logged in it will show a blank page and that's it. You will now need to restart Unity and try again.

If for some reason you do not get this popup then odds are you already have a GitHub credential stored on your machine. In Windows this is stored via the "Credential Manager" and it may be stored under a few different names

![](<../../../.gitbook/assets/image (3).png>)

![](../../../.gitbook/assets/image.png)

![](<../../../.gitbook/assets/image (4).png>)

The above images all show variations of the credential as used. You should be able to force the popup to show again by simply removing any GitHub related credentials already stored in Windows Credential Manager.

Be sure to restart Unity and Unity Hub and then try again.

For note you can also use command line to update your credentials ... Git is fundamentally a command line based tool

{% embed url="https://www.brianchildress.co/update-git-credentials-command-line/" %}

You can read more on the subject here

{% embed url="https://git-scm.com/docs/gitcredentials" %}
