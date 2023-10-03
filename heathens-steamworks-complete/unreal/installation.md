---
cover: ../../.gitbook/assets/Unreal Banner@4x-100.jpg
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Installation

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Engine First

{% hint style="info" %}
We will eventually ship on Unreal Marketplace ... or that is the plan.\
For now though a manual install of a loss Plugin is how we are shipping.\
\
These steps should get you going.
{% endhint %}

### Version

You'll need to install Unreal v5+ we have built the plugin using 5.3 though theoretically... in theory any v5 should play nice.

### C++

You'll need your project to support C++\
No this doesn't mean you have to use C++, but the engine needs to have the project headers and build process of compiling from C++. So you need to do that.

If you chose a C++ project when you created your project congratz, step done, and move on.

If you chose Blueprint project when you created your project, simply add a C++ class via the Tools menu and Unreal Editor will do the work of setting your project up so it can be completed.

### Add the Plugin

So close your engine, and navigate to the project folder, this is where your .uproject file is located.

You should see a .sln file beside it, if you do not then your project is not set up for C++ so go back a step and fix that.

Once you do have a .sln we need to copy the Plugins in. You may already have a Plugins folder if not simply create one.

Next, simply copy the SteamworksComplete folder into your Plugins folder. You'll find the plugin in our GitHub Sponsor Source Repo

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

When done your folder should look similar to the above.

### Rebuild

Right-click on your projects .uproject file and select `Generate Visual Studio Project files`. This will cause the engine to scan the project directory and link up all the related bits we just copied in.

#### Next

So technically you should be able to double-click your project file and it should see the change and compile.

Personally, I prefer to have some control here so I recommend you double-click your .sln file to open the solution in Visual Studio and press Build there.

Note you may see a red X in the log as if something stopped the compilation but if you can press the green play button and it launches and runs the engine then we have what we want.

### Test

So how do we know it's all there and working?\
The simplest way is to open a blueprint editor and see if you can add a Steam node ... just right-click and start typing Steam. You should see a slew of Function nodes we have created for you.
