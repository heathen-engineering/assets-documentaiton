# Unity Install

## Prerequisite Install

{% hint style="success" %}
You must complete the [Register with Discord](../register-with-discord.md) step first, as this will provide you with the zip file we refer to in this step.
{% endhint %}

Extract the zip file to a safe location. If your source is controlling 3rd parties (strongly recommended), the entire `com.discord.partnersdk` folder is what you need. Using Unity Package Manager, install the package ... you can do this by selecting the + button in Unity and selecting the package.json in the `com.discord.partnersdk` folder.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Once done, you should see the Discord Social SDK.&#x20;

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

## Toolkit Install

### Unity Asset Store

If you downloaded from Unity Asset Store, you would install it as typical from the store. The asset will appear in the "In Project" tab of the Unity Package Manager. There, you can select the "Samples" tab and import prefabs and samples.

### GitHub & Patreon

If you are installing from GitHub or Patreon, we recommend you clone the entire repository to your disk for future access.

Using the "Install package from disk..." as you did with the prerequisite, you will browse to the location where you cloned the Source Repo and navigate to `Unity\2025\Assets\Toolkits\com.heathen.discordsocial` to select the `package.json`
