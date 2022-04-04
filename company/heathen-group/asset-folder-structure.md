---
description: Understanding the Heathen Asset folder structure
---

# Asset Folder Structure

{% hint style="info" %}
#### Keep it clean

The whole drive behind this effort is to create cleaner more efficient Unity projects. The idea is you import only what is needed to create your product and omit anything that doesn't need to be compiled into that.

Obviously sample scenes and code are useful for learning but they do not belong in a production project see our [Project Architecture article](../concepts/project-architecture.md) for guidance on how you can keep your production project clean while having access to a superior learning environment.
{% endhint %}

## Introduction

All modern Heathen assets follow a standard folder structure that is designed to help you keep your projects lean and efficient. The idea is that you only import what you need to use, for example in most production projects you would not import the Samples. Prefabs or Documentation folders.

{% hint style="warning" %}
While our assets are not dependent on the location of files; that is you can move things around ; we do use Unity Assembly Definition files.

[https://docs.unity3d.com/Manual/ScriptCompilationAssemblyDefinitionFiles.html](https://docs.unity3d.com/Manual/ScriptCompilationAssemblyDefinitionFiles.html)

As such each folder that contains an Assembly Definition should keep its structure, do not move files in or out of these folder or there children folders or you will cause errors with the resulting assemblies and anything that references them which is most things.
{% endhint %}

## \_Heathen Engineering

This is the root folder for Heathen Engineering, all of Heathen's content will go under this folder. If it is not under this folder it is not Heathen's content.

### 3rd Parties

\_Heathen Engineering/3rd Parties\
Located under the Heathen Engineering root folder this folder will contain unitypackage files for any integrates we may have. These are unitypackage files e.g. you must import them to use them.

### Assets

\_Heathen Engineering/Assets\
This folder will contain sub folders for each product you have installed e.g.&#x20;

* \_Heathen Engineering/Assets/Steamworks
* \_Heathen Engineering/Assets/UX
* \_Heathen Engineering/Assets/SystemCore

Under each product folder you will find the content of that "Unity Asset", that is all of its required components, code, images, models, etc.

### Documentation

\_Heathen Engineering/Documentation\
You should generally omit this folder, it only contains the patch notes for the latest release and a readme.txt for each product telling you to come here to find documentation. This is a requirement from Unity Asset Store and not useful to have in your project in most cases.

### Prefabs

\_Heathen Engineering/Prefabs\
We try to avoid creating prefabs for most of our assets as generally you should be creating your own to meet the needs of your project. That said in some cases we do include prefabs and they will be located here under folders labeled for each product.

### Samples

\_Heathen Engineering/Samples\
This is the location of any demo scenes or example scripts and so forth. In general you should omit this from your import, it is only useful for learning and should not be included in a production project.
