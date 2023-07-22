---
description: Understanding the steam_appid.txt when to use it and when not to use it
---

# 📃 steam\_appid.txt

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

The steam\_appid.txt is a simple text file that contains only your app ID. This is only used during development and for server builds and is located in the "working directory" of the build or editor.

### Example&#x20;

```
480
```

Notice that the file contains nothing but the app ID, no spaces, no comments, and no formatting at all other than the app ID. You should of course use your app ID we are using 480 in this case as an example only.

## When to use steam\_appid.txt

This is required to be used anytime the initializing application is not launched from the Steam client.

{% hint style="warning" %}
This means that steam\_appid.txt must be used when you are:

* Testing a build outside of Steam
* Using the Steam API in your Unity Editor
* Running a server build

Heathen's Steam Settings will check for and create the steam\_appid.txt in your project root anytime you edit the App ID. It will keep the text file updated for you.
{% endhint %}

the steam\_appid.txt is as noted a simple text file that should have nothing in it other than the app id that the Steam API should initialize as. This will cause the Steam API to skip the launched from Steam check and is required to run your game from outside of Steam.

{% hint style="danger" %}
You should not ship the steam\_appid.txt with your game. You generally want your game to test if it was launched from the Steam Client properly, and if not you want your game to close itself and re-launch from the Steam Client.

This however is not a "security" feature, it simply ensures that Steam API can work properly. As you will see with the Overlay and some other features the game must be launched from the Steam Client to work properly.
{% endhint %}

### Dev Testing

The most common use case is to test a local build of your game without bothering to launch it from Steam. This saves you the need to deploy the game to Steam in order to perform simple Dev testing. Note though that because the game is not properly launched from Steam, some features such as the Steam Overlay may not work correctly or at all.&#x20;

Dev Testing aka Unit Testing is usually used to test some small "unit" of code such as a menu behaviour or similar. It is not a full formal test. To properly test your game you will need to deploy it to Steam and download it as your users would.

### Server Builds

Servers (usually) don't have a Steam Client available to them. They are generally run on a server OS that doesn't have a monitor, doesn't have a Steam client and doesn't have a logged-in user. As a result, you need the Steam API to initialize as Steam Game Server,  something Heathen's tool does for you with all Server Builds. You also need the Steam API to skip the launched from Steam Client check e.g. you need to have the steam\_appid.txt located in the working folder of your server build, and populated with your app ID.

{% hint style="info" %}
## What is a Working Folder

Also called the Working Directory it is the root of the program as seen by the process. That is if you were to navigate to the relative path of the program e.g.&#x20;

`./` aka the "root" What folder is that?

That folder is known as the Working Folder or Working Directory. In most cases with a Unity game, the working folder/directory will be the same folder your .exe is located in.
{% endhint %}

## When NOT to use stem\_appid.txt

### Deploying to Steam

If it's deployed from Steam you don't need nor should you use the steam\_appid.txt

### Sending to press

When sending press a build, use Steam's press key system. It's safer for you and lets them download and update from Steam as a real user would.

### Deploying to non-Steam platforms

If it's not a Steam platform then the Steam API should be stripped out of the project.
