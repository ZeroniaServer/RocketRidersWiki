---
layout: post
title: Item Selection
parent: Modification Room
nav_order: 3
---
**Item Selection**
---

<div id="art_image">
    <img src="https://zeroniaserver.github.io/RocketRidersWiki/images/item_selection.png" width="250"  />
</div>

The **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** contains an **Item Selection** interface, with signs to enable or disable each individual **[missile](https://zeroniaserver.github.io/RocketRidersWiki/missiles)** and **[utility](https://zeroniaserver.github.io/RocketRidersWiki/utilities)** item in the game (with certain exceptions described below) as well as entire categories of these items. This allows players to decide which items are obtainable, thus affecting **[Item RNG](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/item_rng)**.

---
### Item Categories

The following categories of items may be configured in the **Item Selection** interface:
- **[Normal Missiles](https://zeroniaserver.github.io/RocketRidersWiki/missiles/normal_missiles)**
- **[Heavy Missiles](https://zeroniaserver.github.io/RocketRidersWiki/missiles/heavy_missiles)**
- **[Lightning Missiles](https://zeroniaserver.github.io/RocketRidersWiki/missiles/lightning_missiles)**
- **[Utilities](https://zeroniaserver.github.io/RocketRidersWiki/utilites)**

Note that **[Special Missiles](https://zeroniaserver.github.io/RocketRidersWiki/missiles/powerups)** cannot be configured for gamemodes like **[Swap Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap)**. Also, any custom items like those obtainable in **[Powerups Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups)** cannot be configured.

There is also an **Enable All Items** sign in the middle of the **Item Categories** section that reenables all applicable item categories and individual items.

At least one **[missile](https://zeroniaserver.github.io/RocketRidersWiki/missiles)** or missile category must be enabled in order for settings to be confirmed (in essence, it is impossible to play with only **[utilities](https://zeroniaserver.github.io/RocketRidersWiki/utilities)**).

---
### Item/Category Locking

When every item in an item category is disabled, the category itself is disabled and *locked*, meaning none of the items in it will spawn and it is not considered for the purposes of **[Item RNG](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/item_rng)**. Enabling one item will reenable its category.

Likewise, when the item category itself is disabled, all the items in it are disabled and locked. Reenabling the category will unlock all of its items and reenable those that were previously enabled.

Certain **[gamemodes](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes)** may override these settings and forcibly lock certain items/item categories in an enabled or disabled state.