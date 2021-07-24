---
layout: post
title: Operator Functions
parent: Behind the Scenes
nav_order: 2
---
**Operator Functions**
---

To make life easier for more technical players of **Rocket Riders**, here are some useful **Operator Functions** you can find and use across all the datapacks in the **[Rocket Riders codebase](https://github.com/ZeroniaServer/RocketRiders)**. Any of these can be run with the command `/function [function:name]`.

Also note that it is preferable to run these in the **Developer team** (`/team join Developer`), which has no restrictions on the player's gamemode or location and minimal interactions with usual game functionality.

---
## `game:forcestop`

This function immediately stops the game and opens the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**. It may be run at any point in the game and is very useful in case things go wrong or if you're done testing in singleplayer.

---
## `game:forcestart`

This function attempts to immediately start the game. It should only be run and will only succeed once game settings have been confirmed in the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**, although it has no harmful effect if run at any other time.

---
## `game:forcecountdown`

This function immediately starts the game countdown, even when the minimum number of players is not met for a countdown to automatically start.

---
## `game:unforcecountdown`

This function reverses the effects of `game:forcecountdown` by reinstating the requirement for a minimum number of players for a countdown to begin.

---
## `game:restartcountdown`

This function restarts the game countdown at 30 (or 10) seconds.

---
## `game:cancelblue` and `game:uncancelblue`

These function disable or enable the Blue team join pad.

---
## `game:cancelyellow` and `game:uncancelyellow`

These functions disable or enable the Yellow team join pad.

---
## `game:uncancelpads`

This function enables all team join pads (including Spectators).

---
## `arenaclear:forceareaclear`

This function forcibly clears and resets the arena, ignoring any **[gamemode-specific arena clearing](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/gamemode_datapacks#arenaclear-folder)** or prerequisite checks that would otherwise occur during a normal **[arena clear](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**. It is not recommended to use this in case prerequisite conditions for arena clearing are not met (see below).

---
## `arenaclear:testvalidclear`

This function attempts to run an **[arena clear](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/arena_clearing)**, but only succeeds if the following prerequisite conditions are met:
- there is at least one **[missile](https://zeroniaserver.github.io/RocketRidersWiki/missiles)** item enabled (see **[Item Selection](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/item_selection)**).
- there is at least one **[gamemode datapack](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/gamemode_datapacks)** installed.

---
## `achievements:reset`

This function resets all **[achievement](https://zeroniaserver.github.io/RocketRidersWiki/achievements)** progress for the executor.

---
## `achievements:roots`

This function grants the root advancements for the executor in each tab of the advancements menu.

---
## `custom:leave`

This function simulates the executor relogging by adding 1 to their `leaveGame` score, thereby putting them back into the Lobby team with the appropriate effects and teleporting them to the Lobby area.

---
## `lobby:parkour/parkoursetup`

This function wipes the **[Parkour](https://zeroniaserver.github.io/RocketRidersWiki/misc/parkour)** leaderboard and all stored times for all players in this **Rocket Riders** world.

---
## `lobby:missiledisplay/givebook`

This function gives the executor a copy of the **[Missile Display Area](https://zeroniaserver.github.io/RocketRidersWiki/misc/missile_display_area)** book, in case the original copy in the lectern is lost or changed.

---
## `rr_[gamemode]:install` and `rr_[gamemode]:uninstall`

These functions will install or uninstall the specified gamemode (ex. `rr_powerups:install` installs **[Powerups Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups)**). See **[`install` and `uninstall` functions](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/gamemode_datapacks#install-and-uninstall-functions)** under **[Gamemode Datapacks](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/gamemode_datapacks)** for more detailed information.

---
## Any others?

Most other functions in the **[Rocket Riders codebase](https://github.com/ZeroniaServer/RocketRiders)** are only designed to be run by the **[Selection armor stand](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/selection_armor_stand)**, as they are not safe for normal operator use.

If you ever find yourself needing to run one of these (and if you know what you're doing), make sure to preface the function call with "`/execute as @e[type=armor_stand,tag=Selection] run `".