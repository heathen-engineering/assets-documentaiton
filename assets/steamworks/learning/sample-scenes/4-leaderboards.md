# 4 Leaderboards

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction&#x20;

This scene demonstrates the use of Steam Leaderboard for setting and reading leaderboards at run time.

![](<../../../../.gitbook/assets/image (159) (1).png>)

### What do I learn?

1. How to use the [Leaderboard Manager](../../components/leaderboard-manager.md)
2. How to use the [Leaderboard Object](../../objects/leaderboard.md)
3. How to set the local user's score for a [Leaderboard](../../objects/leaderboard.md)
4. How to read the local user's score for a [Leaderboard](../../objects/leaderboard.md)
5. How to query entries of other users from a [Leaderboard](../../objects/leaderboard.md)
6. How to access the Knowledge Base (where you are now)
7. How to access the support [Discord ](https://discord.gg/6X3xrRc)
8. How to leave a review 😉

## Objects

### Manager

The manage game object has the [Steamworks Behaviour](../../components/steamworks-behaviour.md) component attached and will handle initialization of the Steam API on start up.

A [Leaderboard Manager](../../components/leaderboard-manager.md) component is attached and configured to use the Feet Traveled [Leaderboard Object](../../objects/leaderboard.md).

### Feet Traveled

From Example Steam Settings as `[LdrBrd] Feet Traveled` this is used to update the leaderboard score and rank

### DEMO SCRIPTS

This contains internal demo scripts used in the scene which are all marked as deprecated. They simply drive the buttons in the menu nothing more.

The demo script works with the [Leaderboard Manager](../../components/leaderboard-manager.md) to upload scores and to handle query results in order to populate the result UI
