---
cover: ../../../../.gitbook/assets/Unreal Banner@2x.png
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

# 🔵 Get Item Definition Properties

{% hint style="success" %}
#### Like what you're seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

While not typically something you should need to do, it is possible to read the properties off of an item definition at run time ... with a few limitations. The main place this comes in handy is when displaying items in a store or similar. Reading the item property for name for example would return the language-specific name of the item if any.

Heathen provides 2 nodes to help with this

### Get Item Definition Properties

This will return an array of all the properties on an item, you shouldn't need to do this in that you should know what properties your items have but it's here if you need it.

### Get Item Definition Property

This will return the value of a given property e.g. "name" for example which is the most commonly used property for this node.

### Item Def

The item to read the properties for

## Example

<figure><img src="../../../../.gitbook/assets/image (16) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
