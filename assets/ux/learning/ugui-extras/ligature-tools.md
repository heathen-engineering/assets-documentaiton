---
description: >-
  Define character combinations and the result character enabling Key Collection
  inputs for Korean, Japanese and other ligature based character sets as well as
  common use extended characters.
---

# Ligature Tools

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

Define character combinations and the result character enabling Key Collection inputs for Korean, Japanese and other ligature based character sets as well as common use extended characters such as translating ( c ) to ©

![](<../../../../.gitbook/assets/image (421).png>)

The Ligature Tools provided in uGUI Extras helps you extend user input to account for common character combinations and to extend the use of Key Collection for language sets that depend on ligatures such as the Korean and Katakana character sets.

The way the system works is that an input string is tested for the input character combinations and when detected that character set is replaced with the output characters.&#x20;

### Ligature Library

Defines a set of ligatures

![](<../../../../.gitbook/assets/image (421).png>)

### Ligature Helper

Connects to a game object with an InputField to parse ligatures on edit of the input field.

{% hint style="info" %}
Works with both Text Mesh Pro Input Field and uGUI standard Input Field
{% endhint %}

![](<../../../../.gitbook/assets/image (486).png>)

## Configuraiton

Configuring ligatures is made simpler with the Ligature Library's custom inspector. You will notice along the top of the inspector several buttons that will auto fill the editor with those settings. You can create custom settings using the **Ligature Editor** fields at the top of the inspector.

## Usage

The typical use is to use the Ligature Library in conjunciton with the Ligature Helper which helps you direct the output of input fields through the Ligature Library to update the input field values as the user types.

An example of this can be seen in the Keyboard examples where you will observer that each input field has a Ligature Helper attached to it

![](<../../../../.gitbook/assets/image (486).png>)

## Code Examples

### Parse Text

{% hint style="info" %}
Note when using Text Mesh Pro ... while Text Mesh Pro renders text in a much better way than Unity's "standard" uGUI text rendering it has some notable limitations, mainly that you must select a sub set of the character set to be supported or create larger Text Mesh Pro font assets.&#x20;

The point is to be aware that Text Mesh Pro fonts rarely support the full unicode character set that traditionaly fonts can.
{% endhint %}

To parse a string in code you can use the library directly

```csharp
var results = library.ParseAll(inputString);
```

The results returned is the result of converting all matching combinations to the target ligature characters.
