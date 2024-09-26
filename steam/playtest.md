---
description: Managing a multi-platform build
---

# 🧪 Playtest

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## &#x20;Introduction

{% hint style="warning" %}
Contrary to the name, a playtest is a separate app, the concept comes from "playtesting" meaning to playtest an idea or small slice/section of the game.\
\
The idea here is that you would create a separate build containing a "verticle slice" of your game something specific you wanted people to playtest.\
\
It is NOT (usually) your full game. it is a small bespoke (for this purpose) section of the game content so that you can "Playtest" that idea in isolation without modifying the main app.\
\
For example, you might want to "Playtest" a boss fight, or a specific dungeon, or a game mode. But you wouldn't playtest the entire game at once (usually).
{% endhint %}

{% hint style="success" %}
If you want to "test" your game as in your main app with people outside of your dev team you would (usually) use a "[Branch](branches.md)" to do that. Offten called a "Beta" you can then issue "Release Override Keys" to allow people to play that branch for some limited period of time or indefinitely your choice.\
\
A branch is a version of your main app, so it uses the same exact configuration and settings as the main app it's just a different version with optionally different key/access such as a Press Build, Alpha or Beta Build, etc.
{% endhint %}

> A Steam Playtest appID has access to the same Steamworks technical features as your main game - but with reduced store and community setup. Instead of having its own separate store page, your Steam Playtest signup will live right on your main game, so that customers can sign up and access the playtest but still Wishlist or Follow the main game.

{% embed url="https://partner.steamgames.com/doc/features/playtest" %}
Valve's documentaiton ... please read it
{% endembed %}

You can set up a playtest for your game at any time once your game has a store page. You can then let players "sign up" for the playtest via a button that will appear on the main app's store page.

<figure><img src="../.gitbook/assets/image (459).png" alt=""><figcaption><p>As seen in Valve's documentaiton ... please read it 😉</p></figcaption></figure>

This is most useful when you want to test a specific part of your game. For example, testing a game mode, a boss fight or some other focused application. it is NOT the way to go to test the entire game.

## Set-Up

{% embed url="https://partner.steamgames.com/doc/features/playtest#2" %}
Valve's litteral step by step guid for doing this ... we will repeate it here
{% endembed %}

1. Create the Playtest app from the Associated Packages & DLC page for your game app![](<../.gitbook/assets/image (460).png>)
2. Configure the app ... \
   At min you will need to provide a Library capsule image and update the visible name of the Playtest App for example `Túatha: Legends - Playtest`
3. Complete the "Release Process" your dashboard will walk you through this

Once that is complete your Playtest is up and ready to work with. You can then make its signup button visible or hidden at will and manage signups by region.
