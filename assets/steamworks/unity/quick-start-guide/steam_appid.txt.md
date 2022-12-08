---
description: Understanding the steam_appid.txt when to use it and when not to use it
---

# steam\_appid.txt

<figure><img src="../../../../.gitbook/assets/512x128 Sponsor Banner.png" alt="Become a sponsor and Do More"><figcaption></figcaption></figure>

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

The steam\_appid.txt is a simple text file that contains only your app ID when used would be located in the working directory of your game.&#x20;

{% hint style="info" %}
Example steam\_appid.txt

```
480
```

As you can see it is a simple text file that contains nothing but the App ID of your app.
{% endhint %}

This is required to be used anytime the initializing application is not launched from the Steam client.

{% hint style="warning" %}
This means that steam\_appid.txt must be used when you are:

* Testing a build out side of Steam
* Using the Steam API in your Unity Editor
* Running a server build

Heathen's Steam Settings will check for and create the steam\_appid.txt in your project root anytime you edit the App ID. It will keep the text file updated for you.
{% endhint %}

the steam\_appid.txt is as noted a simple text file that should have nothing in it other than the app id that the Steam API should initialize as. This will cause the Steam API to skip the launched from Steam check and is required to run your game from out side of Steam.

{% hint style="danger" %}
You should not ship the steam\_appid.txt with your game. You generally want your game to test if it was launched from the Steam Client properly, and if not you want your game to close its self and re-launch from the Steam Client.

This however is not a "security" feature, it simply insures that Steam API can work properly. As you will see with the Overlay and some other features the game must be launched from the Steam Client to work properly.
{% endhint %}

## When to use steam\_appid.txt

### Dev Testing

The most common use case is to test a local build of your game without bothering to launch it from Steam. This saves you the need to deploy the game to Steam in order to perform simple Dev testing. Note though that because the game is not properly launched from Steam, some features such as the Steam Overlay may not work correctly or at all.&#x20;

Dev Testing aka Unit Testing is usually used to test some small "unit" of code such as a menu behavior or similar. It is not a full formal test. To properly test your game you will need to deploy it to Steam and download it as your users would.

### Server Builds

Server's (usually) don't have a Steam Client available to them. They are generally ran on server OS that doesn't have a monitor, doesn't have a Steam client and doesn't have a logged in user. As a result you need the Steam API to initialize as Steam Game Server,  something Heathen's tool does for you with all Server Builds. You also need the Steam API to skip the launched from Steam Client check e.g. you need to have the steam\_appid.txt located in the working folder of your server build, and populated with your app ID.

{% hint style="info" %}
## What is a Working Folder

Also called the Working Directory it is root of the program as see by the process. That is if you where to navigate to the relative path of the program e.g.&#x20;

`./` aka the "root" What folder is that?

That folder is known as the Working Folder or Working Directory. In most cases with a Unity game the working folder / directory will be the same folder your .exe is located in.
{% endhint %}

## When NOT to use stem\_appid.txt

### Deploying to Steam

If its deployed from Steam you don't need nor should you use the steam\_appid.txt

### Sending to press

When sending press a build, use Steam's press key system. Its safer for you and lets them download and update from Steam like a real user would.

### Deploying to non-Steam platforms

If its not a Steam platform then the Steam API should be stripped out of the project.
