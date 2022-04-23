# 3 Stats and Achievements

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)and [Foundation ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-foundation-202671)asset.
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of Steam stats and Steam achievements.

![](<../../../../.gitbook/assets/image (172) (1) (1) (1) (1).png>)

### What do I learn?

1. Importing Stats and Achievements
2. Using Stats and Achievements at run time
3. How to access the Knowledge Base (where you are now)
4. How to access the support [Discord ](https://discord.gg/6X3xrRc)
5. How to leave a review 😉

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

### NumWins

From the Example Steam Settings `[Stat Int] NumWins` this is used by the Add Win button to update the stat value and to display the results

### NEW Achievements 0\_4

From the Example Steam Settings `[Ach] NEW_ACHIEVEMENT_0_4` this is used by the Unlock and Reset buttons to modify the achievement.

### DEMO SCRIPTS

This contains internal demo scripts used in the scene which are all marked as deprecated. They simply drive the buttons in the menu nothing more.
