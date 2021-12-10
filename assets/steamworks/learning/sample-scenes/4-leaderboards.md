# 4 Leaderboards

{% hint style="success" %}
Available in the Steamworks [Complete ](https://assetstore.unity.com/packages/tools/utilities/ux-v2-complete-201905)asset.
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of Steam Leaderboard for setting and reading leaderboards at run time.

![](<../../../../.gitbook/assets/image (157) (1).png>)

### What do I learn?

1. How to set the local user's score for a [Leaderboard](../../objects/leaderboard.md)
2. How to read the local user's score for a [Leaderboard](../../objects/leaderboard.md)
3. How to query entries of other users from a [Leaderboard](../../objects/leaderboard.md)
4. How to access the Knowledge Base (where you are now)
5. How to access the support [Discord ](https://discord.gg/6X3xrRc)
6. How to leave a review 😉

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

### Feet Traveled

From Example Steam Settings as `[LdrBrd] Feet Traveled` this is used to update the leaderboard score and rank

### DEMO SCRIPTS

This contains internal demo scripts used in the scene which are all marked as deprecated. They simply drive the buttons in the menu nothing more.

The demo script has 2 custom functions

1\) Update Score

This simply performs a force update on the leaderboard score based on the value of the InputField

2\) Get Top 10

This queries the board for the top 10 global ranks and prints the results to the console
