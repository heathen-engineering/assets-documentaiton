# Manual Install

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../../company/concepts/become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

If your a GitHub Sponsor you can install Steamworks Complete manually by downloading the source code and simply importing it into your Unity project.

{% hint style="info" %}
Steamworks Complete is dependent on Steamworks.NET and System Core as is noted in the [Prerequisites article](prerequisites.md). If your installing manually so you can avoid needing to fix your Unity Editor's use of Git such as to avoid the "Git Executable Not Found" error ... then know that your still likely to have this issue unless you choose to install everything manually which is likely to create a lot of Human Error issues.
{% endhint %}

## Downloading

As a GitHub Sponsor you can download our full "Source Repo" including all of our code for all our major assets. The easiest and recommended way to download the code is to use [GitHub Desktop](https://desktop.github.com/) and "clone" the repository to your disk.

This is recommended as it will make it easy to "fetch" updates as they occur and keeps things organized as we organize them in the repo.

## Copy & Paste

We do not do any black magic here ... simply copy the desired code into your Unity Project. For Steamworks Complete that would be the whole folder `SourceRepo/Steamworks/com.heathen.steamworkscomplete/`&#x20;

You will notice 2 subfolders `Samples~` and `Tools~` you should remove the `~` character from the end of there name so that Unity can load them in the editor.&#x20;
