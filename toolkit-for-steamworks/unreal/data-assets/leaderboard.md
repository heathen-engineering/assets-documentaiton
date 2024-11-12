---
cover: ../../../.gitbook/assets/Unreal Banner.jpg
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

# Leaderboard

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../where-to-buy/become-a-sponsor.md) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../where-to-buy/become-a-sponsor.md) ... become a sponsor today!
{% endhint %}

## Introduction

Steam Leaderboard a classic feature useful for so much more than simple scoreboards. These can be created in your Steamworks Developer portal or created at run time. In either case, you can represent these as Data Assets for easier referencing and handling in Blueprints.

## Create&#x20;

Create a new Data Asset Instance of type LeaderboardDataAsset

<figure><img src="../../../.gitbook/assets/image (431).png" alt=""><figcaption></figcaption></figure>

## Configure

Set the API Name to the same value you defined in your Steamworks Developer Portal or that you want to be set for this board when created. You can leave the `ID` value default, this will be set at runtime when you `Find` or `Find or Create` this board.

<figure><img src="../../../.gitbook/assets/image (432).png" alt=""><figcaption></figcaption></figure>

## Use

To use the Leaderboard you can simply create a variable of type LeaderboardDataAsset and set its default value to be the instance you just created.

<figure><img src="../../../.gitbook/assets/image (434).png" alt=""><figcaption></figcaption></figure>

With Leaderboards before we try to use them we need to "find" them. This is a Valve concept where we look up the numeric ID of this instance of the board based on its API name. It's important to note that you can only "Find" 1 board at a time, while the process is asynchronous it must be done sequentially.

<figure><img src="../../../.gitbook/assets/image (433).png" alt=""><figcaption></figcaption></figure>

There are two simple options for finding a Leaderboard, the first simply finds an existing board, and the second will create the board if its missing, this allows you to create new Leaderboards at run time useful for player-created maps or content specific to a date such as Summer 2025.

In either case when you find the board you want to update its ID value

{% hint style="warning" %}
#### Remember!

You can only "Find" 1 board at a time, so if you have multiple boards you want to find the ID of you would want to do that sequentially... that is find a board's ID, wait for its event to return that ID, then find the next and so on.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

This ID will persist for the duration of your game session, it will persist through level loads and wont need to be set again. So it is often a good idea to do this on `Bootstrap` of your game for board you know you have and will use, and to do it as soon as possible for boards you know you will need soon.

With this done you can use the Leaderboard variable to work against this specific board

<figure><img src="../../../.gitbook/assets/image (437).png" alt=""><figcaption></figcaption></figure>
