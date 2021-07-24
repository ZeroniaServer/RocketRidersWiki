---
layout: post
title: Gamemode Datapacks
parent: Behind the Scenes
nav_order: 6
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

So, in addition to removing `switchGamemodes` and adding the `swapEnabled` tag (which, by the way, any gamemode datapack will add a tag to the **Selection armor stand** like that when it is enabled), this function also:
- summons a separate marker entity for the Swap timer mechanic
- disables a couple incompatible **[modifiers](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers)**
- disables the usual **[Vortex](https://zeroniaserver.github.io/RocketRidersWiki/utilities/vortex)** functions so that it can run its own functions for the **[ICBM](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap#ICBM)**
- adds another special tag called `respawnFlag` that is way too technical to fully explain but essentially makes it easier to check when players die for the purpose of the **ICBM** giving kill credit

That may have been a bit too in depth of an example, but the point is that the `enable` function ensures any special game configurations are set once the gamemode is enabled.

Likewise, the `disable` function ensures that these game configurations are reverted to their original states (i.e. removes the tags and kills the entities, where applicable). Most importantly, it removes the `[gamemode]Enabled` tag and adding the `switchGamemodes` tag for the next gamemode to be selected. (Hopefully you don't need an example for that.)

---
### `ifenabled` Function

This one gets quite messy, and I'm not even going to try to paste everything into this page. You can read the example `ifenabled` function for **Normal Mode [here](https://github.com/ZeroniaServer/RocketRiders/blob/master/rr_normal/data/rr_normal/functions/ifenabled.mcfunction)**.

To provide some explanation, though: this is basically everything that needs to run whenever the gamemode is actually active. Think of it like the trunk of a "gamemode datapack tree," and all the roots beneath it as all the different functions that need to be run at any moment (whether for starting the game, ending the game, or **[clearing the arena](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**). There's also some special things that need to happen for the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** gamemode selection interface to work, and some other special things to make sure players know what gamemode is currently active. But everything here is pretty standard for any gamemode datapack, and we'll talk about it more later.

---
### `iflast` and `areaclear` Functions

This one is nice and easy. Take a look at `rr_normal:iflast`:
```
execute as @e[type=marker,tag=ArenaClearChecker] at @s run function rr_normal:arenaclear/areaclear
execute if entity @e[type=marker,tag=PlacerClear,tag=!Cleared] run tag @s remove normalLast
tag @e[type=marker,tag=PlacerClear] add Cleared
```

The `iflast` function will always tie into the **[arena clearing](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)** system and make sure to run this gamemode's special `areaclear` function to clean up anything unique to the gamemode from the playing area.

In **Normal Mode**, all that needs to really happen in the `areaclear` function is allowing players to join teams again by removing the `cancelJoin` tag from the join pad entities. However, for other gamemodes like **Powerups Mode**, things like **[Stinging Shields](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups#stinging-shield)** need to be removed from the arena. Therefore, this is a quite important part to have in any gamemode datapack.

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
- summons the gamemode armor stand
- announces the gamemode has been properly installed
- lets the game know that the normal datapack is safely configured by adding 1 to the gamemode armor stand's `CmdData` score
- forcibly stops the game to ensure nothing breaks as a result of gamemode installation (see **[Operator Functions](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/operator_functions))

Generally speaking, you will only ever have to run this kind of a function if there are new gamemodes released as additional downloadable content for existing **Rocket Riders** worlds (*hint hint*). Before that, of course, you will need to run `/datapack enable` for whichever datapack the gamemode corresponds to.

As for uninstallation, see `rr_normal:uninstall`:
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
- instructs the game to forcibly clear the arena the next time settings are confirmed if this gamemode was the last one played
- disables the gamemode
- kills the gamemode armor stand
- refreshes the gamemode IDs of every remaining gamemode armor stand so that there is no gap in IDs
- announces successful uninstallation and prompts the player to disable the datapack
- forcibly stops the game
- refreshes signs in the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**

Generally speaking, you should never have to run this kind of function (and especially never run it for **Normal Mode**!) unless something goes absolutely horribly wrong. It is very ill-advised to run it while the gamemode is enabled and in active play, as the arena will need to be forcibly cleared (which does not include anything special this gamemode may have left in the arena). Do so at your own risk.

---
### TO BE CONTINUED...
I ran out of time to add things for the night. This will be expanded *soon*™