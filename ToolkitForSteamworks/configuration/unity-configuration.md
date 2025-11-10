# Unity Configuration

Open your Project Settings and select Player > Steamworks.

<figure><img src="../.gitbook/assets/image (385).png" alt=""><figcaption></figcaption></figure>

When you first do this, it will create a SteamToolSettings in your project's Settings folder. This is what houses the settings you make in your Project Settings > Steamworks window, and can be source-controlled and shared between projects.

<figure><img src="../.gitbook/assets/image (386).png" alt=""><figcaption></figcaption></figure>

## Active Application

<figure><img src="../.gitbook/assets/image (387).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
You — MUST — restart Unity & Visual Studio when changing your App ID (after previously initialising Steam).\
\
Why?\
This is a requirement enforced by Steam.exe.\
When you initialise Steamworks SDK, the Unity Editor itself and all of its related processes are considered by Steam.exe to be "The Game" ... and you are considered "Playing" until all of that closes out of memory. Thus, you cannot change the initialised App ID without fully restarting Unity.
{% endhint %}

{% hint style="danger" %}
Force-closing Steam.exe will close Unity.\
You — MUST — restart Unity & Visual Studio when changing your App ID (after previously initialising Steam).\
This is not something you can reliably get around.
{% endhint %}

This indicates which Steam Application is active at the moment. By Default, the system will have at least the "Main" and "Demo" applications. This will set a "Scripting Define Symbol" in your Player settings for the selected app ID.

<figure><img src="../.gitbook/assets/image (389).png" alt=""><figcaption></figcaption></figure>

This definition is used in generated code to handle initialisation and access to artefacts such as achievements, stats and leaderboards and can be used in your own code when you have logic that should only apply to 1 of your application IDs.&#x20;

For Example:

```csharp
#if APP480
// code that will only compile when APP480 is active
#else
// code that will only compile when APP480 is not active
#endif
```

## Global

<figure><img src="../.gitbook/assets/image (390).png" alt=""><figcaption></figcaption></figure>

The global section deals with settings unique to the "Parent App", e.g. your main app, that are not duplicated in child apps such as your Demo and Play Tests. It also provides quick access to key resources and, of course, the ability to generate the API wrapper for your specific apps.

### Links

* Knowledge Base\
  This links you to this knowledge base; you will find similar links throughout Heathen's tools linking you to specific articles in the knowledge base.
* Support\
  This links you to the Heathen Group Discord server, where you can find community and live support, share feedback, share your games "Made with Heathen", offer and find freelance help and more.
* Leave a Review\
  thousands of developers, hundreds of games, decades of development, and barely 100 reviews at the time of this writing. Please consider leaving a review for this and any asset you make use of. It's incredibly important for the health of the asset and store, and this is true for really anything you use anywhere ... leave honest reviews.\
  This will open 2 tabs.
  * [TrustPilot](https://ie.trustpilot.com/review/heathen.group)
  * [Unity Asset Store](https://assetstore.unity.com/publishers/5836)

### Generate Wrapper

<figure><img src="../.gitbook/assets/image (391).png" alt=""><figcaption></figcaption></figure>

Pressing this button will read your current configuration and generate the SteamTools.Game static class. This class is what empowers our components, tools and your programmers. It encapsulates all of your configurations and respects the "Active Application", greatly simplifying how you work with Steam even in a multiple-application project, which most will be.

The later articles go into more detail, but for example, you can access a given achievement anywhere in your game logic via its name.

Spacewars Example:

```csharp
SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.Unlock();
```

### Downloadable Content

{% hint style="success" %}
You should "Generate Wrapper" any time you change this value.
{% endhint %}

<figure><img src="../.gitbook/assets/image (392).png" alt=""><figcaption></figcaption></figure>

If your game has Downloadable Content, you can import that information from Steamworks.&#x20;

To do this&#x20;

1. You will need to set your App ID,&#x20;
2. Then, in the editor, press play and initialise Steamworks.&#x20;
3. With your game running and Steamworks initialised, you can click "Import". &#x20;
4. You can now stop the simulation and regenerate your wrapper to add the DLC data.

### Steam Game Server Configuration

<figure><img src="../.gitbook/assets/image (393).png" alt=""><figcaption></figcaption></figure>

Only used if you plan on shipping a "Dedicated Server" build. This configuration allows your dedicated servers to initialise the Steamworks SDK even without a Steam.exe instance logged in and running. You can learn more in the [Steam Game Server](../features/steam-game-server.md) article.

## Main, Demo, Playtests

<figure><img src="../.gitbook/assets/image (395).png" alt=""><figcaption></figcaption></figure>

Your project on Steam is comprised of a "main" application; this is the app ID that was created when you first activated your app credit.

You can, and should also create a Demo. The demo is a "child app" of the main app and does not cost another app credit. Demos are required in order to participate in the Stem Fest events ... you can learn more in the [Launch ](../launch.md)article.

Playtests are similar to a demo in that they are a "child app" of the main; you can have many playtests. These are usually run as free periods during the development phase of your game, where players can access the "Playtest" app, offering you feedback. Each playtest, like the Demo, has its own "build" ... you can learn more in the [Playtest ](../features/playtest.md)article.

Each of these "App IDs" has its own configuration:

### Steam Portal

This link will simply open your browser to your app's Steam Developer portal. Note, this will not work with App 480, as you are not a developer on that app.

### Open Debug Window

This will open the Steamworks Inspector ... useful only when you have the game running in the editor.&#x20;

<figure><img src="../.gitbook/assets/image (394).png" alt=""><figcaption></figcaption></figure>

This window lets you view the internal state and values for various Steamworks artefacts:

* Stats
* Achievements
* Leaderboards
* DLC
* Inventory Items
* Lobbies

### Clear & Set Test Values

The Clear and Set Test Values buttons do as they say and simply clear your current settings or default them to Spacewars settings.

### Application ID

{% hint style="success" %}
You should "Generate Wrapper" any time you change this value.
{% endhint %}

This is where you set the ID for this application. Note that changing the value of the Active Application will cause Unity to recompile, as that is also changing the Scripting Define Symbol.

### Artifacts

{% hint style="success" %}
You should "Generate Wrapper" any time you change this value.
{% endhint %}

The artefacts section outlines all the "parts" of your Steam app.

* Input
  * Sets
  * Set Layers
  * Actions
* Stats
* Leaderboards
* Achievements <mark style="background-color:$warning;">(Can be Imported)</mark>
* Inventory <mark style="background-color:$warning;">(Can be Imported)</mark>
  * Items
  * Bundles
  * Generators
  * Playtime Generators
  * Tag Generators

{% hint style="info" %}
The Steam Inventory Item Definition editor feature from 2025 will be returning to 2026 as a fully revamped feature. The 2026 editor is in development now. \
\
Changes to other systems made the old ScriptableObject-based editor unworkable, so it is not available in 2026.
{% endhint %}
