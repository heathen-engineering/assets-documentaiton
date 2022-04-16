---
description: Creating a clean and efficent project and experimentation environment
---

# Project Architecture

## Introduction

A common problem with many Unity Projects is bloat, by bloat we mean the inclusion of large sums of content and code that serves no purpose in your finished product. Unity's build process will make a valiant attempt to strip down unused code and content but that process is far from perfect and beyond that this bloat adversely impacts your development environment slowing your work and increasing the likelihood of logical errors.

{% hint style="info" %}
#### Logical Error

This is an error that is wrong in that it is not what was intended by the author but doesn't result in an obvious bug or compiler issue.&#x20;
{% endhint %}

To help you keep your project clean and efficient Heathen has defined a standard folder structure making it easy to omit unwanted content such as Sample scenes, Documentation and Prefabs. You can read more about that at the link below.

{% embed url="https://kb.heathenengineering.com/company/asset-folder-structure" %}

## Organization

In practice we recommend that projects that make use of 3rd party assets such as Heathen's assets or any other plugin, Unity Asset Store asset or even Unity's own extensions; has 2 separate Unity Projects.

### Production

This is your core Unity Project and the one that will be used to build your finished product.

{% hint style="danger" %}
We _**very strongly**_ recommend you use a build server and never build a release product on a local workstation.

[Unity's Cloud Build](https://unity.com/features/cloud-build) is an easy to use solution that works with [GitHub ](https://unityatscale.com/unity-version-control-guide/how-to-setup-unity-project-on-github/)and [Plastic SCM](https://unity.com/products/plastic-scm) source control. There are other options if for some reason you don't want to use Unity services.

Save your self a lot of time and frustration by using source control and build services.
{% endhint %}

When importing assets into the project we recommend you omit (**do not import**) sample scenes, demos, and documentation. In most cases you will also want to omit prefabs. The content included in samples and demos is not intended by anyone to be used in a production project.&#x20;

{% hint style="warning" %}
Generally sample code and content is designed and built to be verbose and extraneous for easy understanding and learning. It is not efficient, it is likely to break, intended for a very specific use case and shouldn't be used in production at all.
{% endhint %}

### Experimentation / Learning

This is a second project that should be on the same Unity Version as your Production project. This project should import all of the same assets, plugins, etc. as your production project only this project should fully import the assets including&#x20;

* Documentation
* Samples
* Example Scripts
* Demos
* Prefabs
* etc

The idea is that this project is your place of learning, its your messy sandbox where you don't need to be clean or safe. Ideally you wont modify the demos and examples of the assets you import as this project also serves as a clean example&#x20;
