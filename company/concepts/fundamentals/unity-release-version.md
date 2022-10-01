---
description: This article covers the concepts of Unity target release version.
---

# Unity Release Version

{% hint style="success" %}
#### Like what your seeing?

Consider supporting us as a [GitHub Sponsor](../../become-a-sponsor.md) and get instant access to all our Unity assets, exclusive tools and assets, escalated support and issue tracking and our gratitude.\
\
These articles are made possible by our [GitHub Sponsors](https://github.com/sponsors/heathen-engineering) ... become a sponsor today!
{% endhint %}

## Introduction

This article is not directly related to a Heathen asset but is a common question when asking what version of the engine you should be using.

{% hint style="info" %}
Heathen always builds its assets to run on the oldest LTS version in active support at the time of that particular release.

**For example:**\
From Q2 2021 to Q2 2022 Heathen will build and release on 2019 LTS\
From Q2 2022 to Q2 2023 Heathen will build and release on 2020 LTS\
From Q2 2023 to Q2 2024 Heathen will build and release on 2021 LTS\
\
This is due to how Unity runs its LTS support. We will adjust this standard as required to conform to Unity's long term support plan such that Heathen assets are always built to support the oldest version of Unity that Unity its self actively supports.

Note that in some cases older versions of Unity might work as we do actively try to avoid using programming features that are engine version specific however we cannot assure or fully support these cases as Unity doesn't fully support the underlying engine and we are ultimately an extension of Unity's engine.
{% endhint %}

## What

It is Heathen's suggestion that you should be building your project with the intent that it will release on the most recent version on Unity LTS that is available at the time of its initial release. This requires you to have an understanding of Unity's planned road map which is always subject to change but does follow a rough pattern of releasing the prior year's LTS at the end of Q1 in any given year.

### Examples

| Release Quarter | Target Unity Version (assumes normal release pattern) |
| --------------- | ----------------------------------------------------- |
| Q3 2021         | 2020 LTS                                              |
| Q4 2021         | 2020 LTS                                              |
| Q1 2022         | 2020 LTS                                              |
| Q2 2022         | 2021 LTS                                              |
| Q3 2022         | 2021 LTS                                              |
| Q1 2023         | 2021 LTS                                              |
| Q2 2023         | 2022 LTS                                              |

Hopefully the above pattern is clear. If followed this would insure your project is released on the most recently available version of Unity at the time of that projects initial release giving it the maximum amount of time under long term support from Unity.

## Why

{% embed url="https://unity3d.com/unity/qa/lts-releases" %}

Unity's stated plan with its major release versions and its support cycle revolves around the pattern of 2 years of on going "long term" support for a version from its initial release. Do keep in mind that this is a guide line not a hard fact, for example 2018 LTS remained in support longer than expected.

If you follow this pattern however you can insure that your released project has 2 years of active and on going maintenance and support backed by Unity being the developer of the underlying engine and that is in general good. It means that any bugs you or your users discover that is an underlying problem with the engine is likely to get fixed by Unity.

If you release on a version that is out of LTS and you or your users discover a bug that is an underlying issue with the Unity engine then Unity support is most likely going to ask you to upgrade to the next available LTS version of the engine which means a major version upgrade for your released game project and in general that should be avoided as it can be difficult and lead to further issues.

## When

When should you upgrade?\
Use cases follow; please remember these are guide lines, written here to help you get started on thinking about your project and community. You should consider your own project, your team and your goals.

**Use Case 1**\
****My project is nearly complete but is built on an older version of Unity.

This is the use case that our recommendation as stated above attempts to avoid. Ideally you would have been upgrading your project while your project was in active development keeping it on the closest available version of the Unity engine to the LTS version you expect to release on.

Since that is no longer possible you need to do the assessment. Is it more important to you that you have Unity backed LTS and how long do you expect that. Compare that importance with how important it is that you hit your currently planned release date. Note that a major Unity engine update can add a lot of time to development and testing and is likely to push a near by release date back.

**Use Case 2**\
My project is in active development but is being built on an older version of Unity.

Why are you on an older version of Unity?

Unless you have a good answer for that which is of greater value to you than having LTS and arguably a more efficient and more stable platform to work on then you should probably be upgrading.

**Use Case 3**\
My project is already released on an older version of Unity, I'm doing a patch now, should I upgrade?

Is your patch a major update where your aiming to extend the life of your project?\
Do you have bugs/issues with the current version?\
Do you have plans to use features or tools only available in newer versions?

These are the sorts of questions to be asking your self/team.&#x20;

Question 1:\
Releasing a major patch with the goal of revitalizing your project and extending its long tail is a good time for doing a major update to the engine. This would increase the LTS you have available, improve the longevity of your project by using more modern technology but it may also result in the loss of users that are bound to older machines as newer versions of Unity do tend to raise the minimal requirements.&#x20;

In this case you could choose to release your patch as an optional update. With Steam this could be done by maintaining the "legacy" version and releasing a new app ID with the new version that you ask Valve to grant to all owners of the original legacy version. You can then delist the legacy version.

You see this sort of behavior with games like Divinity Original Sin. Its original version ran for some time, they released an "Enhanced" edition and delisted the older original version insuring new customers could only buy the new version while old customers could still download the old version.

Question 2:\
In this case you probably want to upgrade but not necessarily to the latest possible version assuming you don't want to change the minimal requirements for the game and you want to reduce risk upgrade breaking additional aspects of your game.&#x20;

In this case we would likely choose to upgrade to the nearest version of Unity that resolves the bug, though we would probably also consider Question 1 and 2 to try and maximize our return on investment.

Question 3:\
This question is a value assessment, is the new feature worth the time to upgrade and the potential loss of users that are them selves dependent on older versions of Unity due to hardware limitations.

