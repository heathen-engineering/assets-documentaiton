# 🌳 Branches

{% hint style="success" %}
#### Like what you're seeing?

Consider supporting us as a [GitHub Sponsor](../become-a-sponsor/) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="success" %}
Want to test your game ... yes even before its released?

\
This is the way to do it.\
\
Branches are useful for more than just testing, but they are the gold standard for full-game testing as well.
{% endhint %}

{% embed url="https://partner.steamgames.com/doc/store/application/branches" %}
Valve's documentation on the subject
{% endembed %}

Branches can be created from your Builds page in Steamworks developer portal. You can define as many as you need ... for example, if you want to test in phases (Alpha 1, Alpha 2, etc.) or if you want a simpler Test Build vs Live Build setup you can do that too.

## Test Release

So you want to use a branch to have people outside of your development team test your game?

{% embed url="https://partner.steamgames.com/doc/features/keys" %}

To give them access you will need to generate a key for them. Keys are described in more detail in the page linked above but in short

* Yes you can issue a key for a specific branch
* Yes you can revoke keys

## What about Playtest?

A playtest is a separate app and has some crossover with the concept of a Beta branch. the below cards list some "rules of thumb" but of course, your mileage may vary. There is also the concept of Early Access to consider so keep that in mind as well.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><h3><a href="playtest.md">Playtest</a></h3></td><td><ul><li>Best before release not usually used post-release.</li><li>Want the test to be open to everyone or to a very large group 2,000 or more</li><li><p>Would benefit from a separate app e.g. a focused test</p><ul><li>Stress test</li><li>Game Mode test</li><li>Game Mechanic test</li><li>Boss test</li></ul></li></ul></td></tr><tr><td><h3>Branch</h3></td><td><ul><li>Want to be highly selective over who gets access</li><li>Want to test the full game e.g. "Beta Access"</li><li>Want to run phased testing of the main game (Alpha 1, Alpha 2, Alpha 3, etc.)</li><li>Want to run separate build testing post-release</li></ul></td></tr></tbody></table>



The main thing to keep in mind is that with a Branch the player is playing on the "main app" so they are simply playing a different version of your main game.

For a playtest they are playing a separate app, some factors do cross over for easy setup but by in large a playtest is an isolated app configuration and package.
