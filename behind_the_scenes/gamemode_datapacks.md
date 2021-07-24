---
layout: post
title: Gamemode Datapacks
parent: Behind the Scenes
nav_order: 7
---
**Gamemode Datapacks**
---

So remember how we were talking about that wacky little **[Selection Armor Stand](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/selection_armor_stand)** earlier? (If not, you should totally read that page first!)

Well... not everything in that page was correct. In fact, there's a little bit more going on to make the game work. And maybe a little more armor stands. (We're sorry, marker lovers!)

---
## Introducing... **GAMEMODE DATAPACKS!**

So, when you pull back the curtains and turn off the smoke machines, each **[gamemode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes)** is actually its own little datapack. The datapack folders and their namespaces are all prefixed by `rr_`, with the abbreviated name of the gamemode after. For instance, the **[Powerups Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups)** datapack is called `rr_powerups` internally, and the **[Capture the Flag Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)** datapack is called `rr_ctf`.

Each of these datapacks also have their own little armor stand. Not as cool as the **[Selection armor stand](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/selection_armor_stand)**, of course. But these armor stands are in the same obscure corner of the Lobby, have tags named after their gamemodes (so the **Powerups** one has the tag `rr_powerups`, for example), and may have other tags or scoreboard data associated with them for their respective gamemodes. The game knows that a gamemode is "installed" (more on that later... or you can skip down [here](#install-and-uninstall-functions)) when this armor stand is present.

More than that, each gamemode datapack has a standardized set of files and folders that define how the game operates in different states and configurations (for instance, which teams players can join, which items are given, where players spawn, how you win the game, etc.). During development, this system of architecture was key to modularizing the common functionalities of each gamemode. (Say that sentence ten times fast!)

---
## The Gamemode Datapack Structure

The easiest way to examine the structure of gamemode datapacks is by looking at the **[`rr_normal` datapack](https://github.com/ZeroniaServer/RocketRiders/tree/master/rr_normal)**, which should *always* be active in any **Rocket Riders** world.

First off, there is a `#minecraft:tick` function tag defined with the following contents:
```json
{
 "values": [
 "rr_normal:everytick"
 ]
}
```

`rr_normal:everytick` is a function that runs every tick the gamemode datapack exists for. Let's take a look at that:
```
execute as @e[type=armor_stand,tag=rr_normal] run function gamemodes:updateid
execute if score @e[type=armor_stand,tag=Selection,tag=!normalEnabled,tag=switchGamemodes,limit=1] SetGamemode = @e[type=armor_stand,tag=rr_normal,limit=1] gamemodeID run function rr_normal:enable
execute if score @e[type=armor_stand,tag=Selection,tag=normalEnabled,tag=switchGamemodes,limit=1] SetGamemode = @e[type=armor_stand,tag=rr_normal,limit=1] gamemodeID run tag @e[type=armor_stand,tag=Selection,limit=1] remove switchGamemodes
execute as @e[type=armor_stand,tag=Selection,tag=normalEnabled] run function rr_normal:ifenabled
execute as @e[type=armor_stand,tag=Selection,tag=normalLast] run function rr_normal:iflast
```

Okay, that's a lot. The basic gist: each gamemode armor stand has its own ID which gets assigned based on how many gamemode armor stands are present in the world. This is used to switch between gamemodes in the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**.

When **Normal Mode** is selected, it runs the function `rr_normal:enable` once, and after that, it runs the function `rr_normal:ifenabled` every tick for which it is enabled. Then, if it was the previously selected gamemode (for the purposes of **[arena clearing](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**, generally speaking), it runs the function `rr_normal:iflast`.

So what do those functions do exactly? Let's go one by one.

---

### `enable` and `disable` Functions
`rr_normal:enable` contains the following:
```
tag @e[type=armor_stand,tag=Selection] remove switchGamemodes
tag @e[type=armor_stand,tag=Selection] add normalEnabled
```

Basic enough, right? Well, not quite. This is where any other gamemode datapack would do other fancy things with the **[Selection armor stand](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/selection_armor_stand)**, setting certain tags and possibly summoning certain entities that are key to making the gamemode work. For instance, this is what `rr_swap:enable` does:

```
tag @e[type=armor_stand,tag=Selection] remove switchGamemodes
tag @e[type=armor_stand,tag=Selection] add swapEnabled
summon marker 12 55 0 {Tags:[swapplatform]}
tag @e[type=armor_stand,tag=Selection] add SurpriseEggOff
tag @e[type=armor_stand,tag=Selection] add SplashStreamsOff
tag @e[type=armor_stand,tag=Selection] add vortexOverride
tag @e[type=armor_stand,tag=Selection] add respawnFlag
```

So, in addition to removing `switchGamemodes` and adding the `swapEnabled` tag (which, by the way, any gamemode datapack will add a `[gamemode]Enabled` tag to the **Selection armor stand** like that when it is enabled), this function also:
- summons a separate marker entity for the Swap timer mechanic.
- disables a couple incompatible **[modifiers](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers)**.
- disables the usual **[Vortex](https://zeroniaserver.github.io/RocketRidersWiki/utilities/vortex)** functions so that it can run its own functions for the **[ICBM](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap#ICBM)**.
- adds another special tag called `respawnFlag` that is way too technical to fully explain but essentially makes it easier to check when players die for the purpose of the **ICBM** giving kill credit.

That may have been a bit too in depth of an example, but the point is that the `enable` function ensures any special game configurations are set once the gamemode is enabled.

Likewise, the `disable` function ensures that these game configurations are reverted to their original states (i.e. removes the tags and kills the entities, where applicable). Most importantly, it removes the `[gamemode]Enabled` tag and adds the `switchGamemodes` tag for the next gamemode to be selected. (Hopefully you don't need an example for that.)

---
### `ifenabled` Function

This one gets quite messy, and I'm not even going to try to paste everything into this page. You can read the example `ifenabled` function for **Normal Mode [here](https://github.com/ZeroniaServer/RocketRiders/blob/master/rr_normal/data/rr_normal/functions/ifenabled.mcfunction)**.

To provide some explanation, though: this is basically everything that needs to run whenever the gamemode is actually active. Think of it like the trunk of a "gamemode datapack tree," and all the branches and leaves connecting to it as all the different functions that need to be run at any moment (whether for starting the game, ending the game, or **[clearing the arena](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**). There's also some special things that need to happen for the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** gamemode selection interface to work, and some other special things to make sure players know what gamemode is currently active. But everything here is pretty standard for any gamemode datapack, and we'll talk about it more later (or click [here](#game-folder) to skip to that section).

---
### `iflast` Function

This one is nice and easy. Take a look at `rr_normal:iflast`:
```
execute as @e[type=marker,tag=ArenaClearChecker] at @s run function rr_normal:arenaclear/areaclear
execute if entity @e[type=marker,tag=PlacerClear,tag=!Cleared] run tag @s remove normalLast
tag @e[type=marker,tag=PlacerClear] add Cleared
```

The `iflast` function will always tie into the **[arena clearing](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)** system and make sure to run this gamemode's special `areaclear` function to clean up anything unique to the gamemode from the playing area (see [`arenaclear` Folder](#arenaclear-folder)).

---
### `install` and `uninstall` Functions

So now, let's go back to those armor stands. In order for a gamemode datapack to operate, they need to exist in the world. But in order for that to happen, they need to be summoned first. More than that, any important scoreboard objectives need to be created for the gamemode datapack to operate. This is where the `install` function comes into play. Take a look at `rr_normal:install`:
```
execute unless entity @e[type=armor_stand,tag=rr_normal,limit=1] run summon armor_stand 25 184 -6 {Tags:["rr_normal","gamemodeAS"],Marker:1b,Invisible:1b,Invulnerable:1b,CustomNameVisible:0b,CustomName:'{"text":"Normal Mode"}'}
execute if entity @e[type=armor_stand,tag=rr_normal,limit=1] run tellraw @s {"text":"Normal Mode installed.","color":"green","bold":true}
scoreboard players add @e[type=armor_stand,tag=rr_normal,limit=1] CmdData 1
execute unless entity @e[type=marker,tag=PlacerClear] run function game:forcestop
```

In essence, this function:
- summons the gamemode armor stand.
- adds any necessary scoreboard objectives (not applicable here).
- announces the gamemode has been properly installed.
- lets the game know that the normal datapack is safely configured by adding 1 to the gamemode armor stand's `CmdData` score.
- forcibly stops the game to ensure nothing breaks as a result of gamemode installation (see **[Operator Functions](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/operator_functions)**).

Generally speaking, you will only ever have to run this kind of a function if there are new gamemodes released as additional downloadable content for existing **Rocket Riders** worlds (*hint hint*). Before that, of course, you will need to run `/datapack enable` for whichever datapack the gamemode corresponds to; that way, Minecraft recognizes all the functions it contains.

As for uninstallation, take a look at `rr_normal:uninstall`:
```
tag @e[type=armor_stand,tag=Selection,tag=normalLast,limit=1] add needsForceClear
tag @e[type=armor_stand,tag=Selection,tag=normalLast,limit=1] remove normalLast
function rr_normal:disable
execute if entity @e[type=armor_stand,tag=rr_normal,limit=1] run kill @e[type=armor_stand,tag=rr_normal,limit=1]
scoreboard players reset * gamemodeID
execute unless entity @e[type=armor_stand,tag=rr_normal,limit=1] run tellraw @s {"text":"Normal Mode uninstalled.","color":"red","bold":true}
execute unless entity @e[type=armor_stand,tag=rr_normal,limit=1] run tellraw @s {"text":"Click here to disable the Normal Mode datapack (recommended).","color":"red","underline":true,"clickEvent":{"action":"run_command","value":"/datapack disable \"file/rr_normal\""}}
execute unless entity @e[type=marker,tag=PlacerClear] run function game:forcestop
scoreboard players add @e[type=armor_stand,tag=Selection,limit=1] refreshsigns 1
```

In essence, this function:
- instructs the game to forcibly clear the arena the next time settings are confirmed if this gamemode was the last one played.
- disables the gamemode.
- kills the gamemode armor stand.
- refreshes the gamemode IDs of every remaining gamemode armor stand so that there is no gap in IDs
- announces successful uninstallation and prompts the player to disable the datapack.
- forcibly stops the game.
- refreshes all the signs in the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** now that the gamemode is no longer installed.

Generally speaking, you should never have to run this kind of function (and especially *never* run it for **Normal Mode**!) unless something goes absolutely horribly wrong. It is very ill-advised to run it while the gamemode is enabled and in active play, as the arena will need to be forcibly cleared (which does not include anything special this gamemode may have left in the arena). Do so at your own risk.

---
### `game` Folder

Assuming the [`ifenabled` function](#ifenabled-function) is configured correctly, there should be three functions in the `game` folder of the datapack that run depending on the current state of the game:

- `gamestart`, which runs every tick regardless of if the game has started or not. This function generally regulates starter gear the players receive, joinable teams, and countdown events.
- `ingame`, which runs every tick once the game has started. This function generally regulates **[Item RNG](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/item_rng)**, spawnpoints, win conditions, and custom mechanics for the gamemode.
- `gameend`, which runs for 570 ticks once the game has ended. This function generally empties the players' inventories, resets tags and scores, announces relevant match statistics, and kills unnecessary entities.

There may be other functions in the `game` folder depending on what other functionalities the gamemode requires; this varies heavily from datapack to datapack. However, these three functions should *always* be in the `game` folder and should be called by the `ifenabled` function.

---
### `arenaclear` Folder

Assuming the [`iflast` function](#iflast-function) is configured correctly, there should be two functions in the `arenaclear` folder of the datapack which run during and after an **[arena clear](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**: `areaclear` and `baseplacement`.

The `areaclear` function is run when an arena clear is actively taking place. In **[Normal Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/normal)**, all that needs to really happen in the `areaclear` function is allowing players to join teams again (by removing the `cancelJoin` tag from the join pad entities). However, for other gamemodes like **[Powerups Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups)**, custom utilities like **[Stinging Shields](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups#stinging-shield)** need to be properly removed from the arena. Therefore, this is a quite important part to have in any gamemode datapack.

The `baseplacement` function is run after an arena clear has taken place and configures the arena for the next selected gamemode. In **[Swap Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap)**, for instance, this function decides which team is Dark and which team is Light, while also setting the correct blocks in the newly placed bases. In **[Capture the Flag Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)**, this function converts the bases from glass into concrete and places four flagpoles. For any gamemodes that make changes to the arena or require some initial setup before the game starts, this function is incredibly important.

There may be other functions in this folder than just the two mentioned above. These functions generally relate to things like the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**, where settings may need to be disabled and locked if incompatible with that gamemode. There may also be extra functions for removing specific things from the arena or placing specific things into the arena, which depends heavily on the needs of the gamemode.

---
### `everytick` Folder

While not present in the `rr_normal` datapack nor required for every gamemode datapack, some gamemode datapacks have an `everytick` folder. As in the **[`rocketriders` datapack](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/rr_datapack)**, the functions in this folder generally serve miscellaneous purposes (like ensuring players get **Piercing Pickaxes** in **[Capture the Flag Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)**) or dictate custom **[utility](https://zeroniaserver.github.io/RocketRidersWiki/utilities)** functionality. This is very flexible and depends heavily on the needs of the gamemode.

---
### `items` Folder

This might sound a bit familiar... anyway... While not present in the `rr_normal` datapack nor required for every gamemode datapack, some datapacks have an `items` folder. As in the **[`rocketriders` datapack](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/rr_datapack)**, the functions in this folder dictate which items the players may receive and how **[Item RNG](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/item_rng)** works for the given gamemode.

The `rr_powerups` datapack has an `items` folder for all the possible powerups the player may receive in **[Powerups Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups)** and the RNG that selects which item to give when.

Similarly, the `rr_swap` datapack has an `items` folder for the custom **[utilities](https://zeroniaserver.github.io/RocketRidersWiki/utilities)** and the per-team item sets in **[Swap Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap)**.

Once again, the functions in this folder depend heavily on the needs of the gamemode. If the gamemode does anything custom with item sets, then it should probably have an `items` folder.

---
### `info` and `tip` Functions

The last things all gamemode datapacks should have are:

- an `info` function, which is simply a list of `tellraw` commands that print information about the game in chat (run upon clicking the *Gamemode Info* sign in the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_roomm)**).
- a `tip` function, which announces relevant **[tips](https://zeroniaserver.github.io/RocketRidersWiki/misc/tips)** for the given gamemode in chat.

Assuming the [`ifenabled` function](#ifenabled-function) is configured correctly, these functions run on their own and perform the expected functionality.

---
### Anything Else?

Well, gamemode datapacks are datapacks, after all; they may contain other things than just what was mentioned above.

Sometimes, they'll have other folders for organizing functions (like the `baseswap` folder in `rr_swap`) or overriding other specific functionalities (like the `achievements` folder in `rr_chase`).

Sometimes, they'll include loot tables and item tags if they add custom items, or advancements if they require advanced detection techniques for anything or add new **[custom achievements](https://zeroniaserver.github.io/RocketRidersWiki/achievements)**.

Sometimes, they may have something completely different than anything I just wrote!

It really depends on who's writing them and what the gamemode needs, which is the beauty (if you're willing to call it that) of the whole system!

---
## Final Notes

If you made it to the end of this page and actually understood any of it, congratulations on being a complete nerd! You earned yourself an imaginary gold star.

For real, though: We encourage you to look around in the **[Rocket Riders Codebase](https://github.com/ZeroniaServer/RocketRiders)** and see what you can find in all the gamemode datapacks. Who knows, maybe you could even write one of your own someday!

*(Okay, yeah, good luck with that...)*