---
description: Quick start guide for Heathen's Blockchain Game SDK
---

# Quick Start Guide

{% hint style="info" %}
Before you get going with the Unity integration, you need to contact Arkane and set up your account. From them you will get your **Application ID**, **Client ID** and **Secret** all of which you will need to use the Unity integration.

[https://arkane.network/](https://arkane.network/)
{% endhint %}

## Step 1: Register with Venly

For this step you simply need to contact Arkane and set up an account.&#x20;

{% embed url="https://arkane.network/" %}

## Step 2: Installation

Follow the installation steps out lined on this page then return to this guide.

{% embed url="https://kb.heathenengineering.com/assets/bgsdk/bgsdk-install" %}

## Step 3: Configuration

### Creating your Settings

![](<../../../.gitbook/assets/image (37).png>)

Right click in your Unity Project tab and select **Create > Blockchain Game SDK > Settings**

### Applying your IDs

Select the newly created BGSDK Settings object and populate the `Application ID`, `Client ID` and `Client Secret` fields with the values provided to you by Arkane Networking during your account set up.

![](<../../../.gitbook/assets/image (38).png>)

## Step 4: Creating Artifacts

By artifacts we mean creating your contracts and token definitions. To do so simply select the `Model` tab on the BGSDK Settings object you created and click the `Add Contract` button to create a new contract. Within the contract you click a `+` button to create a new token. You will notice the Contract and Token objects are created as Scriptable Objects in your project folder next to your BGSDK Settings object. You can remove contracts or tokens by clicking the `-` button.

![Screen shot of the sample BGSDK Settings object included with the samples.](<../../../.gitbook/assets/image (39).png>)

## Step 5: Artifact Settings

Select your contract artifacts and configure the settings as desired. Note the system will link the tokens created under the contract for you.

![Screen shot of a contract from the samples](<../../../.gitbook/assets/image (40).png>)

Select your token artifacts and do the same, the Contract field will already be set for you

![SCreen shot of a token from the samples](<../../../.gitbook/assets/image (41).png>)

## Step 6: Synchronize

{% hint style="danger" %}
This action cannot be undone. It will commit the settings you have applied and upload them to the chain. It will also read any contracts and tokens on the chain and pull them down into the Unity Project. Be sure your contract and token settings are configured as desired before you click this button.
{% endhint %}

Synchronize is a button on the BGSDK Settings object. Clicking this button will first check the chain for contracts and tokens and create those objects in your Unity project, linking them with anything already existing. Next it will read any contracts and tokens linked to the settings object that are not already on the chain and create them on the chain.

This step cannot be undone. Be sure your settings are as desired before you click Synchronize.
