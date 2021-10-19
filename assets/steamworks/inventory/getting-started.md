---
description: >-
  Getting started with Steam Inventory via Heathen Engineering's Steam Inventory
  Manager tools
---

# Getting Started

## **Introduction**

First, you should understand what Steam Inventory is and is not, the only real place to do so is via Valve's documentation and videos on the feature.&#x20;

{% embed url="https://partner.steamgames.com/doc/features/inventory" %}

You will also need to understand the Steam Inventory Schema, while Heathen's tools help you define your item definitions in this schema there will be time when you need to manually edit to take advantage of more complex features, or to apply some unique concept specific to your project.

{% embed url="https://partner.steamgames.com/doc/features/inventory/schema" %}

## **Step 1: Set up**

Make sure you have your Steam Settings object created and linked with a Steamworks Behavior component.

![Screen shot of the example settings provided with the package.](<../../../.gitbook/assets/image (34).png>)

**You can access the Inventory Editor by clicking the "Editor" button to the left of the Inventory header **

![](<../../../.gitbook/assets/image (35).png>)

## **Step 2: Defining your Steam Item model**

![](<../../../.gitbook/assets/image (30).png>)

{% hint style="info" %}
**\[CreateAssetMenu…]** line above the class name. this defines the menu we will click to create a new one of these. remember it you are going to use it a lot. If you want to put it with the other inventory items, the path should look like\
\
`[CreateAssetMenu(menuName = “Steamworks/Player Services/<name it>”)]`
{% endhint %}

You should create one or more `Item Model` objects as appropriate to your game. An item model object is simply a class derived from `InventoryItemDefinition` and can be added to the Inventory Editor window by dragging and dropping it on the window where it will appear as an item.

The asset does include an example item, but this example item is a bare bones example of creating a custom item. In general you should define your own types as appropriate to your game. A few examples follow that might be used in an RPG or similar

### Examples

#### Consumable

This would represent any item that can be consumed by the player. It would express an icon for visualization in inventory UI screens as well as effect data, e.g. what effect does it have when consumed you could also provide type information such as Food, Drink, Potion, Poison, etc.

```csharp
namespace AlwaysUseANameSpace
{
    [CreateAssetMenu(menuName = “Custom Item Types/Consumable”)]
    public class ConsumableItemDefinition : InventoryItemDefinition
    {
        public enum Type
        {
            Food,
            Drink,
            Potion,
            Scroll,
            Poisen
        }
        
        public struct Effect
        {
            public enum Target
            {
                HealthRegineration,
                ManaRegineration,
                StaminaRegineration,
                HeathMax,
                ManaMax,
                StaminaMax,
                AttackPower,
                AttackSpeed,
                SpellPower,
                CastSpeed
            }
        
            public Target target;
            public float value;
        }
    
        public string displayName;
        public string description;
        public Image icon;
        public Type type;
        public Effect[] effects;
    }
}
```

#### Weapon

This could represent a weapon that characters can use, similar to Consumable we might have an icon and type but we would also want a prefab so we can know what to spawn in the world when something is using this weapon.

```csharp
namespace AlwaysUseANameSpace
{
    [CreateAssetMenu(menuName = “Custom Item Types/Weapon”)]
    public class WeaponItemDefinition : InventoryItemDefinition
    {
        public enum Type
        {
            Sword,
            Axe,
            Mace,
            TwoHanderSword,
            TwoHanderAxe,
            TwoHanderMace,
            Bow,
            Staff
        }
    
        public string displayName;
        public string description;
        public Image icon;
        public Type type;
        public int level;
        public float damage;
        public float speed;
        public GameObject prefab;
    }
}
```

## **Step 3: Building your model**

![](<../../../.gitbook/assets/image (31).png>)

Now that all the hard parts are done, we can get to the fun parts. On your Steam Settings object click the ‘Editor’ button beside the Inventory header as shown above. This will open the Steam Inspector tool on the Inventory Editor tab with the settings you opened it from already set.

You will notice a few empty lists on the left side and a green drop box in the bottom left corner. This drop box is where you will drop items, generators, bundles, and tag generators that you create. Dropping them there will add them to the settings object and let you edit the ItemDef attributes within them. Remember ItemDef is how Steam sees it, so, this tool is helping you create the JSON schema that Valve wants you to upload.

Next you need to create your items. You can do this all at once if you like, that is you can create a scriptable object for each item and then select them all and drop them on the drop box to add them. As noted, you have different types of items. In Step 2 you created a custom Item of type Item. Confusing I know but that is how Valve defines it,  that is it’s a regular simple item as opposed to a Bundle of items and Item Generator or a Item Tag Generator. The other special types are already defined for you because they do not usually have any special data in Unity. If you really want to create your own you can simply derive from ours.

{% hint style="info" %}
Note you might have noticed a list item for Recipes, but that recipes you create do not drop in the box. This is because we only list recipes you use, so you need to add the recipe to 1 or more items, generators, or bundles for it to show up. To do so create your Recipe object in your Asset Database and then drag it to the Exchange drop box on an Item, Item Generator or Bundle.
{% endhint %}

## **Step 4: Defining your attributes**

![](<../../../.gitbook/assets/image (33).png>)

Now that you have your items listed you will notice a lot of them are red. This indicates they have some error. You can select each item and see why its red, that is the fields on it will be red if they are in error. At first the main error you have is that they all have the same ID where each one must have a unique ID.

You should also add all the attributes appropriate for your item. For example if you want it to be available for sale then you need to add a Price **or** Price Category - note the **or** - don't add both.

{% hint style="success" %}
We suggest you use a number pattern. For example, you could say that all items are in the 10000 range, all bundles are in the 1000 range and all generators are in the 2000 range. So, your first simple item might be 10001. This is not required but it will save you some headache down the road if you have some pattern to your IDs.
{% endhint %}

In the case of Items, Bundles and Generators you can add a range of attributes to them by clicking the ‘Add Empty’ button at the top right of the window. At minimal all items should have a name so be sure to add the Name attribute. For full details on what each attribute does see Valve’s documentation; [https://partner.steamgames.com/doc/features/inventory/schema](https://partner.steamgames.com/doc/features/inventory/schema)

## **Step 5: Uploading your Schema to Valve's partner site**

This is nice and easy. Once you have your model laid out or simply updating an existing model you can generate the JSON Valve expects by clicking the Generate JSON button in the upper right.&#x20;

{% hint style="warning" %}
Note the button will be green if the model is good. If its red them something in your model is wrong, you can fix it by selecting the red record. This will show you what field isn't right.
{% endhint %}

Once you have your JSON generated navigate to [https://partner.steamgames.com/apps/inventoryservice/](https://partner.steamgames.com/apps/inventoryservice/1024120)\<YourAppId> you could also browse to this by logging into your partner portal and going to App Admin, Community, Inventory Service. Toward the bottom you will see a field 'Item Definitions' you can upload the JSON there.&#x20;

{% hint style="warning" %}
Note that if you get an error such as Error Code 2 the most likely case is that your missing some required attribute. The most common one being Name - note that everything must have a name.
{% endhint %}

## Step 6: Using your items

Now that you have items defined in your Steam Developer Portal, and you have representations of those items in your Unity Project linked with your Steam Settings the Heathen Steamworks SDK will help you manage the player's inventory.

In most cases you will access the items them selves to check for quantity owned by the player or to perform actions such as starting a purchase or consuming an item. You can also use the `SteamworksInventoryTools` static class to perform these actions.

{% embed url="https://kb.heathenengineering.com/assets/steamworks/inventory/examples" %}
