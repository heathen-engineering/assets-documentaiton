# ☕ Team Collaboration

{% hint style="success" %}
#### Like what your seeing?

Support us as a [GitHub Sponsor](../../../become-a-sponsor/) and get instant access to all our assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](../../../become-a-sponsor/) ... become a sponsor today!
{% endhint %}

## Introduction

{% hint style="info" %}
Find our Example Git Repository [here](https://github.com/heathen-engineering/ExampleTeamRepo)!
{% endhint %}

{% hint style="success" %}
Before you get started [read this! (IMPORTANT)](git-control-and-unity.md)
{% endhint %}

When your working with a team and need to share assets from a secure repository such as Heathen's Source Repo.

When you sponsor Heathen you get a site based license, which means you are licensed to have other staff, contractors, etc. who are working under you on your project use our code for that project/task.

Getting them access can be a challenge since they will not have access to Source Repo and you cannot give them access to it without them paying for a sponsorship

The solution however is much easier than bothering with that and is the recommended practice rather or not your using any secure assets.

## Solution

In your GitHub Repo simply create a folder named `Third Party` or something suitable for your to understand the contents are 3rd party files.&#x20;

{% hint style="danger" %}
This should not be a folder inside your Unity Project it is keenly important that the files in this folder are not changed at all and Unity if it imports them it may modify the metadata breaking links and references and preventing correct function.
{% endhint %}

Once you have them copied into your repository check them in such that you have a repo that looks similar to this

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Once checked in you can import the package to your Unity Project using the Git URL

### Git URL Structure

Simply take the URL you see in the browser for the folder that contains the package.json in our example case that is

```
https://github.com/heathen-engineering/ExampleTeamRepo/tree/main/ThirdParty/com.heathen.steamworksfoundation
```

Next replace `/tree/main` with `.git?` such that the URL looks like this

```
https://github.com/heathen-engineering/ExampleTeamRepo.git?/ThirdParty/com.heathen.steamworksfoundation
```

This is the `Git URL` that can be used with Unity Package Manager's `Add from Git URL` feature.

Once you add the package the URL will be reflected there as well meaning future updates are a matter of clicing the Update button.

{% hint style="info" %}
Obviously you would need to copy in the source update into your ThirdParty folder and check in before clicking Update in order for it to see the updated files.
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (15) (1) (2).png" alt=""><figcaption></figcaption></figure>
