---
layout: post
title: The rocketriders Datapack
parent: Behind the Scenes
nav_order: 3
---
**The `rocketriders` Datapack**
---

The `rocketriders` datapack is the main brains of the game! (Besides the **[Selection armor stand](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/selection_armor_stand)**, of course.) You can find it **[here](https://github.com/ZeroniaServer/RocketRiders/tree/master/rocketriders/data)** on the **Rocket Riders codebase**.

A quick glance at the datapack will reveal that it is a massive, sprawling mess. (Well, so was the development of the game... art imitates life, or something like that.)

This page will attempt (keyword: *attempt*) to give a high level overview of the purposes and contents of each folder of the datapack, starting from the most basic and going up to the most advanced.

The functions and files themselves are all named after their respective purposes and commented to the best of our limited abilities as developers, so feel free to read into those more on your own time and see what you can gather!

---
## `minecraft` Folder

This might not be the simplest to explain, but it makes the most sense to start out with.

The `minecraft` folder is used to define a `#minecraft:tick` function tag with the function `everytick:everytick`, and a `#minecraft:load` function tag with the function `custom:upon_load`. Minecraft is able to recognize these function tags and run the contained functions as specified.

The `everytick:everytick` function is run every tick, as the name quite heavily implies, and is the source of all code execution (apart from advancements with function rewards, anyway) in the entire datapack. See [`everytick` Folder](#everytick-folder) for more information.

The `custom:upon_load` function, on the other hand, runs upon the world or datapacks reloading. For now, this simply resets the positions of the **[credits armor stands](https://zeroniaserver.github.io/RocketRidersWiki/misc/credits_armor_stands)** in the Lobby, but it has been a quite useful development tool for initializing scoreboard objectives and such.

On a slightly-less-relevant note, the `minecraft` folder also contains a recipe override for `repair_item`, which acts to disable the ability to repair items. This is a quick hackfix to prevent players from combining their **Shooting Sabers** or something and getting bows without enchantments.

---
## `custom` Folder

This folder contains the `upon_load` function mentioned above, as well as any custom predicates and item/block tags used liberally by the game for various purposes (e.g. detecting players in the void, clearing player inventories, replacing any blocks that could have come from a missile during **[arena clears](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**).

---
## `tutorial` Folder

This folder contains all the functions, advancements, and location predicates relating to the functionality of **[tutorial achievements](https://zeroniaserver.github.io/RocketRidersWiki/misc/tutorial_achievements)**.

---
## `lobby` Folder

This folder contains all the functions (plus one little loot table) for the **[credits armor stands](https://zeroniaserver.github.io/RocketRidersWiki/misc/credits_armor_stands)**, **[Missile Display Area](https://zeroniaserver.github.io/RocketRidersWiki/misc/missile_display_area)**, **[Parkour Area](https://zeroniaserver.github.io/RocketRidersWiki/misc/parkour)**, **[Navigation Book](https://zeroniaserver.github.io/RocketRidersWiki/misc/navigation_book)**, and pretty much any other interactive elements of the main Lobby.

---
## `gamemodes` Folder

This folder contains several functions that are crucial to the operation and integration of **[gamemode datapacks](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/gamemode_datapacks)** (yes, those exist) with other parts of the game.

---
## `modifiers` Folder

This folder contains all the functions necessary for **[modifiers](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers)** to work, including what actually runs ingame when a modifier is active, selecting modifiers in the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**, disabling all modifiers, and seeing information about each modifier.

---
## `achievements` Folder

This folder contains all the advancements and related functions used to reward **[custom achievements](https://zeroniaserver.github.io/RocketRidersWiki/achievements)** to players. The advancements themselves are split into several subfolders:
- `rr_challenges`, for the individual icons and descriptions of each achievement
- `rr_easy`, for the root and end-row advancements for the Easy Achievements tab
- `rr_medium`, for the root and end-row advancements for the Medium Achievements tab
- `rr_hard`, for the root and end-row advancements for the Hard Achievements tab
- `rr_utility`, for any advanced checks that can only be performed by advancement criteria (sometimes not even for achievements, but other things like **[Nova Rockets](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)** launching players)

The functions, on the other hand, are all grouped together. There is a function for each achievement that requires constant checks and a `gain` function that makes each player in the game run all of those separate functions every tick.

There are also functions to dictate the conditions under which achievements may be rewarded at the end of the game, those being `aftergame`, `aftergameblue` and `aftergameyellow`.

Some other functions exist there for the purpose of resetting all-time or per-round achievement progress (these may be run by operators; see **[Operator Functions](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/operator_functions)**). Also, any functions rewarded by utility advancements from the `rr_utility` subfolder are included here.

---
## `items` Folder

This folder contains all the functions and loot tables used for giving items (see **[Item RNG](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/item_rng)**) and spawning **[missiles](https://zeroniaserver.github.io/RocketRidersWiki/missiles)** (see **[Missile Spawning](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/missile_spawning)**) in the base game.

There are also functions here for preventing item duplication, making **[modifiers](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers)** like **Surprise Egg**, **Wind Down**, and **Minute Mix** work, and tracking where missiles have been spawned for the purposes of **[arena clearing](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**.

---
## `game` Folder

This folder contains all the functions used to control game states and events like the countdown before the game starts, what happens during the game, and what happens when the game is ending, as well as giving players starter gear, controlling join pads, killing players in the void, and the like.

There are also functions (and an advancement) here used to determine whom to reward kill credit to when a player has been killed indirectly by a **[utility](https://zeroniaserver.github.io/RocketRidersWiki/utilities)** item such as a **[Nova Rocket](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)** or **[Vortex](https://zeroniaserver.github.io/RocketRidersWiki/utilities/vortex)**.

---
## `arenaclear` Folder

This folder contains all the functions used to clear the arena (see **[arena clearing](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)** for an in-depth look at how this works!), set down new bases with **[base decorations](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/base_customizer)**, and make the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** functional as a whole.

From a top down view, think of the `game` folder as accounting for about three quarters of the actual game loop (starting the game, playing the game, and ending the game) and the `arenaclear` folder accounting for the last quarter (preparing a new game).

---
## `everytick` Folder

This folder generally contains all the functions that must run every tick (as the name implies), including the aforementioned `everytick:everytick` function at the root of all code execution.

This is too broad to properly narrow down, but the most concrete examples are that all the functions for **[utilities](https://zeroniaserver.github.io/RocketRidersWiki/utilities)** are located in this folder, as well as anything for handling new players/relogs, preventing fall damage, preventing item dropping, and preventing players from entering the Nether.

The `everytick:general_settings_and_hotfixes` function is also used for many miscellaneous purporses driving certain functionalities of the Lobby, giving necessary effects/tags/scores to players, and ensuring some utilities work as intended.

Although this could easily be said for any of the last few sections, without this folder, the rest of the game just could not operate.