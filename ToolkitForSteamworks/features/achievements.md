# Achievements

## Introduction

Achievements are a simple and traditional feature for games that can help drive player engagement. They can also act as a poor man's Game Statistics feature, for example, you can set achievements to unlock at particular milestones and then monitor the game's global stats to see what % of your player base has unlocked each achievement, giving an idea of how your game's retention looks.

<details>

<summary>Useful Links</summary>

* Valve's Documentation\
  [https://partner.steamgames.com/doc/features/achievements](https://partner.steamgames.com/doc/features/achievements)

</details>

## Quick Start

First, you need to create your achievements on the Steam Developer portal. [https://partner.steamgames.com/](https://partner.steamgames.com/)

### Create

Log in to your Steam Developer Portal and access your app's admin page. Look for the Technical Tools section and select the Edit Steamworks Settings option.

<figure><img src="../.gitbook/assets/image (236).png" alt="Techincal Tools"><figcaption></figcaption></figure>

From there, select the Stats & Achievements > Achievements option and create your new achievements.&#x20;

Make a note of the value you use in the API Name field. You will use it when working with achievements in code.&#x20;

In Unity, if you prefer to work with Achievements via an object reference then you can use our AchievementObject which is a Unity ScriptableObject that can be referenced and accessed like any other Unity Object.

<figure><img src="../.gitbook/assets/image (237).png" alt="Achievement test"><figcaption></figcaption></figure>

### Publish

You \*\***MUST**\*\* publish your changes in Steam Developer Portal before they will be accessible via Steam API. In the Steam Developer Portal when you have pending changes you will see a red banner at the top of the screen ... click it and follow the instructions.

<figure><img src="../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

## Using Achievements

The first thing to understand is that with stats and achievements, the process of setting them in two steps.

1. You assign the value&#x20;
2. You store the changes in the backend

{% hint style="success" %}
Understand that not every game needs achievements, that if you're going to have achievements, they should be part of the game and not an afterthought you bolted on because why not? Meaningless achievements can harm the user experience by breaking immersion or simply drawing attention away during gameplay.

The following are some ideas for meaningful achievements and how you might tie those achievements into other aspects of your game.
{% endhint %}

### Storing Stats and Achievements

This is the process of committing any changes made during gameplay to the Steam backend. That is, you can freely "set" the state of achievements and stats during gameplay, such as incrementing kills of enemy units, player score, etc. These changes are written to the local cash, not directly to the backend.

When the game is closed or when you call "Store", the changes will be committed to the backend. This should be done at key points in the game, such as at the end of a level, on player death, when a boss is defeated or at some other opportune time. It is generally not recommended that you constantly call Store() with each change.

{% hint style="warning" %}
Think about when you want that pop-up to show\
It will be immersion-breaking, it could cover parts of the screen, and it could cause things such as Windows Auto HDR to cause screen flicker ... in generally you want it to show only when the player is not actively engaged in gameplay such as on a menu, debriefing, "You Died" screen, etc.
{% endhint %}

There are several ways to store stats and achievements, and they all do the same thing. They are simply different ways you can trigger the effect, depending on what objects you have available in memory and how you are more comfortable as a developer.

### Pop up

The Steam pop-up that you're used to seeing when you unlock an achievement or receive some other notification is not code in the game but rather the Steam client rendering overtop the game's window.&#x20;

{% hint style="info" %}
Players can force this to be disabled, so do not assume it will always be present. It's the user's choice as configured in the Steam client, not your game. This is not for you to control.
{% endhint %}

For achievements, this popup triggers when an achievement is [stored ](achievements.md#storing-achievements)not when it is set. Also, note that because it is rendering over the game window it will not likely work properly when testing in the Unity Editor or if you have a debugger or other app mounted to the process, as this may restrict window updates and or add additional windows to the process.

### New Player Experience

Think of your achievements like a meta quest ...&#x20;

{% hint style="info" %}
Meta means beyond or above, etc., and when we use it, we mean a concept, information, etc. that is not part of the main but additional and external to it.
{% endhint %}

Like a meta quest, that is a quest for the player (not the character in-game world) to learn your game. To encourage them to explore the features and functions of your game in a structured manner and to offer some non-gameplay impacting rewards for doing so.

For a practical example of this, see DOTA 2's "New Player Experience" aka "Welcome Quests" where they present "quests" for new players to do simple things like open menus, use features, review information, play each of the game modes, etc. Importantly, this is not hidden from the player it's presented to the player in the menu, just like a quest, showing what steps are yet to be done and which have been done.

{% embed url="https://www.youtube.com/watch?v=GtstEl0ULu4" %}
Not sponsored/promoted, this is just a random video on the topic of DOTA 2 Welcome Quests you might find relevant
{% endembed %}

### Player Tutorial

The best tutorials are fun and engaging parts of the game that happen to also teach the player mechanics, concepts, demonstrate tactics and strategies and more. Similar to the New Player Experience approach, you can use Achievements as a means to draw attention to these instructions and reward their completion without forcing the player into them.

### Item Rewards

Steam Inventory is a huge topic in itself that needs its own guide. The overlay with Achievements is that you can restrict eligibility for Item Promotion drops based on unlocked achievements. You can use this with New Player Experience or Tutorial style achievements to award in-game items for completing the tasks.

### Achievement Hunters

There are many types of players and a common one across all game genres is the "Collector" or "Hunter" This is a type of player that likes to "100%" the game. Be careful not to bloat your game with meaningless achievements, as this will simply frustrate the collector, but do make sure to track and reward them for fully exploring your game.

### Player Retention Monitoring

Did you know you can view the global stats for games that have achievements seeing what % of the player base has achieved each achievement?

<figure><img src="../.gitbook/assets/image (239).png" alt=""><figcaption></figcaption></figure>

Well, now you do, this means you can use achievements to understand (vaguely) what parts of your game are used and what are not, used well, and you can track where players "fall off".

## Creating Achievements

> #### [Valve](https://partner.steamgames.com/doc/features/achievements)
>
> Steam Stats and Achievements provides an easy way for your game to provide persistent, roaming achievement and statistics tracking for your users. The user's data is associated with their Steam account, and each user's achievements and statistics can be formatted and displayed in their Steam Community Profile.

Achievements like stats are created in your [Steam Developer Portal](https://partner.steamgames.com/), once created there you can access them via their ID, if you are not using Heathen's Steamworks ... why aren't you, it has a free version. Then you can import your Stats and Achievements into Unity or use our AchievementData structure to easily work with your achievements in code.

Valve's documentation on the [Stats and Achievement](https://partner.steamgames.com/doc/features/achievements) features is a good place to get started.

## Examples

### Set Achievement

Setting an achievement is a 2 step process, you first "set" the achievement that is you mark it to be "unlocked". This step can be done in real-time as your game plays and even calls multiple times a frame with no adverse impact on performance as this is NOT calling the backend at all, it simply records locally that this achievement should be set.

Then, at an appropriate time for your game, such as at the end of a boss fight, on player death, end of a mission, before or after a cut scene, etc., you would call "Store" aka "Store Stats". This will cause Steam to commit the changes for all stats and achievements to the backend. It is at this time that notifications pop up. This should NOT be called rapidly, such as with every frame, it should only be called at key points in your game.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Achievement modular component to work with achievements in your game.&#x20;

<figure><img src="../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>

You can also use it to unlock the achievement from Unity Events or similar&#x20;

<figure><img src="../.gitbook/assets/image (404).png" alt=""><figcaption></figcaption></figure>

## C\#

Access your achievements via the [Generated Wrapper](../configuration/unity-configuration.md#generate-wrapper)

```csharp
// Unlock the achievement
SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.Unlock();
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (242).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
bool result = SteamUserStats()->SetAchievement(StringCast<ANSICHAR>(*apiName).Get());
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
SteamUserStats.SetAchievement(achievementApiName, achieved);
```
{% endtab %}
{% endtabs %}

### Read Achievement

Typically, when "reading" an achievement, you are simply checking if the achievement is "achieved" aka "unlocked" for the user and this is a simple boolean value. You can, however read additional information, such as when it was unlocked, you can also get the current "icon" for the achievement which will be either the locked or unlocked version depending on if the user has achieved this achievement.

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Achievement modular component to work with achievements in your game.&#x20;

<figure><img src="../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>

Use the drop-down to select which achievement you want to work with. You can then add fields:

<figure><img src="../.gitbook/assets/image (402).png" alt=""><figcaption></figcaption></figure>

To set one or more Icon, Name or Description UI elements.

<figure><img src="../.gitbook/assets/image (403).png" alt=""><figcaption></figcaption></figure>

## C\#

{% code fullWidth="true" %}
```csharp
// Unlock the achievement
bool isAchieved = SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.IsAchieved;

// Get Achievement Name
string displayName = SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.Name;

// Get Achievement Description
string descriptionText = SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.Description;

// Get when it was unlocked
DateTime? unlockTime = SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.UnlockTime;

// Get the image for the achievement
SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.GetIcon(texture =>
{
    // texture is the Texture2D for this achievement
});
```
{% endcode %}
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (246).png" alt=""><figcaption></figcaption></figure>

## Achievement Data Asset

<figure><img src="../.gitbook/assets/image (247).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
//Get the unlock state and time
bool achieved;
uint32 unixTime;
SteamUserStats()->GetAchievementAndUnlockTime(StringCast<ANSICHAR>(*apiName).Get(), &achieved, &unixTime);

//Optionally get the percentage complete if relevant
float pert;
SteamUserStats()->GetAchievementAchievedPercent(StringCast<ANSICHAR>(*apiName).Get(), &pert);

//Get the Achievement's display name
FString name = FString(SteamUserStats()->GetAchievementDisplayAttribute(StringCast<ANSICHAR>(*apiName).Get(), "name"));
//Get the Achievement's description
FString desc = FString(SteamUserStats()->GetAchievementDisplayAttribute(StringCast<ANSICHAR>(*apiName).Get(), "desc"));
// Get the Achievement's hidden status
const char* DisplayAttribute = SteamUserStats()->GetAchievementDisplayAttribute(StringCast<ANSICHAR>(*apiName).Get(), "hidden");
//Convert the hidden status string to a bool
bool isHidden = (DisplayAttribute && strcmp(DisplayAttribute, "1") == 0);
//Clean up our buffer for the hidden status attribute
delete[] DisplayAttribute;

// This is just an example of using all the data you just gathered
// It's assuming "status" is something that needs all this data
status.Achieved = achieved;
status.Percent = pert;
status.UnlockTime = FDateTime::FromUnixTimestamp(static_cast<int64>(unixTime));
status.Name = name;
status.Description = desc;
status.IsHidden = isHidden;

//Get the Icon ... you can do this with the aid of our SteamGameInstance
// Note the "callback" is a 
DECLARE_DYNAMIC_DELEGATE_OneParam(FIconLoadCallback, UTexture2D*, icon);
//First you need to get the image handle
int32 handle = SteamUserStats()->GetAchievementIcon(StringCast<ANSICHAR>(*apiName).Get());
SteamGameInstance->LoadIcon(handle, apiName, callback);
```
{% endtab %}

{% tab title="Steamworks.NET" %}
<pre class="language-csharp"><code class="lang-csharp">//Read the value
SteamUserStats.GetAchievement(achievementApiName, out bool achieved);

//Read the value and time
var result = SteamUserStats.GetAchievementAndUnlockTime(achievementApiName, out bool achieved, out uint epoch);
var unlockTime = new DateTime(1970, 1, 1).AddSeconds(epoch);

//Get Icon
//First you need to manage the native callback
if (m_UserAchievementIconFetched_t == null)
    m_UserAchievementIconFetched_t = Callback&#x3C;UserAchievementIconFetched_t>.Create(HandleIconImageLoaded);

//Fetch the image handle
var handle = SteamUserStats.GetAchievementIcon(achievementApiName);

//If the handle is valid
if (handle > 0)
{
    //Find the image size
    if (SteamUtils.GetImageSize(handle, out uint width, out uint height))
<strong>    {
</strong><strong>        //Create a Texture2D
</strong>        Texture2D pointer = new Texture2D((int)width, (int)height, TextureFormat.RGBA32, false);
        //Set a buffer to fit the data
        int bufferSize = (int)(width * height * 4);
        byte[] imageBuffer = new byte[bufferSize];
        //Get the RGBA of the image
        if (SteamUtils.GetImageRGBA(imageHandle, imageBuffer, bufferSize))
        {
            //Read and flip the data for Unity
            byte[] result = new byte[buffer.Length];

            int xWidth = (int)(width * 4);
            int yHeight = (int)(height);

            for (int y = 0; y &#x3C; yHeight; y++)
            {
                for (int x = 0; x &#x3C; xWidth; x++)
                {
                    result[x + ((yHeight - 1 - y) * xWidth)] = buffer[x + (xWidth * y)];
                }
            }

            //Load the data and apply it to the texture
            pointer.LoadRawTextureData(result);
            pointer.Apply();
        }
    }
}
else
{
    Debug.LogWarning("No image available");
}
</code></pre>
{% endtab %}
{% endtabs %}

### Clear Achievement

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Achievement modular component to work with achievements in your game.&#x20;

<figure><img src="../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>

You can also use it to clear the achievement from Unity Events or similar&#x20;

<figure><img src="../.gitbook/assets/image (405).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
// Clear the achievement
SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.Clear();
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (248).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
bool result = SteamUserStats()->ClearAchievement(StringCast<ANSICHAR>(*achievementApiName).Get());
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
SteamUserStats.ClearAchievement(achievementApiName);
```
{% endtab %}
{% endtabs %}

### Store Changes

{% tabs %}
{% tab title="Toolkit for Unity" %}
## Code Free

You can use the Achievement modular component to work with achievements in your game.&#x20;

<figure><img src="../.gitbook/assets/image (399).png" alt=""><figcaption></figcaption></figure>

You can also use it to store the achievement from Unity Events or similar.

{% hint style="success" %}
This will store all modified stats and achievements.
{% endhint %}

<figure><img src="../.gitbook/assets/image (406).png" alt=""><figcaption></figcaption></figure>

## C\#

```csharp
// Store all modified stats and achievements
SteamTools.Game.Achievements.ACH_TRAVEL_FAR_ACCUM.Store();
```
{% endtab %}

{% tab title="Toolkit for Unreal" %}
## Blueprint

<figure><img src="../.gitbook/assets/image (250).png" alt=""><figcaption></figcaption></figure>

## C++

```cpp
SteamUserStats()->StoreStats();
```
{% endtab %}

{% tab title="Steamworks.NET" %}
```csharp
SteamUserStats.StoreStats();
```
{% endtab %}
{% endtabs %}
