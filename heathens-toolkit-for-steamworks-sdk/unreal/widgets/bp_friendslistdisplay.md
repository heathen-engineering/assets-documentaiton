---
cover: ../../../.gitbook/assets/Unreal Banner@2x.png
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

# BP\_FriendsListDisplay

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

An example of reading and displaying a user's friends in a manner similar to the native Steam Friends List. This blueprint will demonstrate the process of getting a user's Friend Groups and available Friends, sorting them based on groups and status and displaying them in a UI Widget.

Everything here is done using Blueprint nodes, the same process can be used in C++ where the function names and use will all match those described here.

<div align="left">

<figure><img src="../../../.gitbook/assets/image (353).png" alt=""><figcaption></figcaption></figure>

</div>

The control mimics Steam's friend list presenting the user's "Friend Groups" also known as "Friend Tags" as well as 2 common use groups for all "Online" and "Offline" friends.

In the example above you can see we have a custom group "Family" which contains 3 users all of which are offline at this time. The Family Group is a custom tag I created and applied to the friends who are part of my actual family. I have also given these friends Nicknames so when they display for me I see those nicknames as opposed to the account name everyone else would see.

## Construction

Reviewing the Graph for the example will uncover how it was built.

### Construct / Destruct

<figure><img src="../../../.gitbook/assets/image (351).png" alt=""><figcaption></figcaption></figure>

The example scrip binds and unbinds to the Steam Persona State Change property on construct and destruct respectively.

When the result event is run the Update Display event is called causing the widget to rebuild its display.

### Update Display

<figure><img src="../../../.gitbook/assets/image (352).png" alt=""><figcaption></figcaption></figure>

When the update display process starts its first task is to clean up the widget's internal state and prepare to reload the friends list. To simplify the display and reduce duplication of friends in the list we use Unreal Sets to help us track who has and hasn't been displayed yet.

* Displayed Friends\
  Populated during the first phase of the load when we iterate over the player's custom Friend Groups (friend tags). This will be a list of all the friends that are displayed in a custom group and thus don't need to be displayed in the general purpose "Online" or "Offline" groups
* Online Friends\
  We will populate this list after populating Displayed Friends and it will contain all friends who are currently not offline and who were not recorded in the Displayed Friends set
* Offline Friends\
  We will populate this list after populating Displayed Friends and it will contain all friends that are currently listed as offline and who were not recorded in the Displayed Friends set

<figure><img src="../../../.gitbook/assets/image (354).png" alt=""><figcaption></figcaption></figure>

The For-Each loop that ends the clean-up process is iterated over the "Friend Groups" the user has. For each entry in the array, we will get the display name of the group and the array of members in the group. With that information, we can create a new BP\_FriendsListGroup widget and add it to the Custom Groups widget which is a vertical list panel so will simply stack these up for us.

During this process, we add the array of members found in each group to the Displayed Friends set. We will use this later to exclude these friends from being displayed in the more common Online and Offline groupings.

<figure><img src="../../../.gitbook/assets/image (355).png" alt=""><figcaption></figcaption></figure>

When the For-Each loop completes we will get an array containing all of the local user's "Immediate" friends. This is how Steam identifies the "normal" friends of a user e.g. those that are immediately available.

We will again iterate over this list but this time we are simply sorting them, first we check if they are not in the Displayed Friends set e.g. we haven't already displayed them. If not we will get their persona state and check if they are Online or Offline sorting them into the Offline Friends set and Online Friends set.

<figure><img src="../../../.gitbook/assets/image (356).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (357).png" alt=""><figcaption></figcaption></figure>

With the sorting completed, we simply use the Offline and Online sets to update our general use groups (Online and Offline).

First, we check if the sets are empty, if so we simply hide that grouping as there is nothing to show there.

If it's not empty we ensure it's visible and call the [BP\_FriendsListGroup](bp\_friendslistgroup.md) Show Users function to have it update the displayed list of users.
