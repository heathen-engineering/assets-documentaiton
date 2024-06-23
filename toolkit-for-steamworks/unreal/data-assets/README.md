---
cover: ../../../.gitbook/assets/Unreal Banner.jpg
coverY: 0
---

# Data Assets

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Unreal has a concept of Data Asset where we can define an asset representing the type of data in our project, add variables, events and functions to that type, and then create "records" of this type as assets in our project that can easily be referenced in blueprints and on actors.

This is an incredibly flexible and powerful feature of the Unreal engine and Heathen's Toolkit for Steamworks makes use of it to simplify working with common Steam artefacts. We have defined a Primary Data Asset type for each of the common Steam artifacts listed in the articles below.

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

## Create Assets

To create a new Data Asset please refer to Unreal's documentation for the version of the engine you are using.

{% embed url="https://dev.epicgames.com/documentation/en-us/unreal-engine/data-assets-in-unreal-engine" %}
Documentaiton for 5.4 to help you get started
{% endembed %}

## Use Assets

Each asset has its own uses and is described in detail in its own article ... please see the navigation panel on the left side of this page.

In general, you would create a data asset for each "entry" of that type. For example, if you have 3 achievements you had defined in Steamworks Developer Portal then you would create 3 AchievementDataAsset instances 1 for each of the achievents you defined.

Once you have the Data Asset Instance created you can now reference it in your Blueprints and other objects as a variable. To do so simply create a new variable and set its type to be the type of the instance in question, for our achievements this would be a variable of type AcvehievementDataAsset.

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Once you compile your blueprint you can set the default value of your variable to the instance you created. You can now drag off the variable as you would any other variable and use that artefact and its member functions in a context-sensitive manner.

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Aside from reducing the number of Function Libarry nodes, you would need to perform the same action without the context of a Data Asset, each Data Asset has further benefits unique to its specific artifact type. In the example for we are getting the quantity of Iron Ingots the player owns, to do this without context would require multiple asynchronous operations to fetch the data from Steam and then loops to sum up the details found if any.
