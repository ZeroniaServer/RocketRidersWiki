---
layout: post
title: Game Rules
parent: Modification Room
nav_order: 2
---
**Game Rules**
---

In the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**, players can control several settings that apply broadly to any **Rocket Riders** games and further customize their playing experience in the section labeled **Game Rules**.

Below is a list of these game rules, a description of their effects, and the conditions under which they may be configured.

---
### Pierce Prevention

When enabled, this prevents **[missiles](https://zeroniaserver.github.io/RocketRidersWiki/missiles)** from being spawned inside of portals, which would normally be able to end the game. This is enabled by default.

Note that this setting is inapplicable in both **[Capture the Flag](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)** and **[Chase Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/chase)**, as neither gamemode has portals.

---
### Snipe Portals

When enabled, this allows **[Fireballs](https://zeroniaserver.github.io/RocketRidersWiki/utilities/fireball)** and **[Nova Rockets](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)** to be used to directly explode enemy portals. This is disabled by default.

Note that, when enabled, you still cannot use these items to explode your own portal.

Also note that this setting is inapplicable in both **[Capture the Flag](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)** and **[Chase Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/chase)**, as neither gamemode has portals.

---
### Tie/Sudden Death

When enabled, this allows ties and **[Sudden Death](https://zeroniaserver.github.io/RocketRidersWiki/misc/sudden_death)** periods to occur. This is enabled by default.

Note that this setting is inapplicable to **[Capture the Flag](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)** and **[Chase Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/chase)**, as neither gamemode has portals.

Also note that this setting is disabled for **[1v1 Duel Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/duel)**, as the gamemode itself is a best of three match.

---
### Item Delay

This setting allows players to configure the delay between receiving items from a minimum of 5 seconds to a maximum of 30 seconds. Clicking on the sign brings up a message in chat with clickable text to change the item delay in increments of 1 to 5 seconds. By default, the item delay is 15 seconds.

Note that this setting is inapplicable when the **[Minute Mix](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers#minute-mix)** modifier is enabled, as the item delay is set to 60 seconds and players receive sets of 8 items at a time.

Also note that this setting is affected by **[Sudden Death](https://zeroniaserver.github.io/RocketRidersWiki/misc/sudden_death)** periods and the **[Wind Down](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifier#wind-down)** modifier, which reduce item delay to even lower limits than 5 seconds.

---
### Hotbar Limit

When enabled, this setting prevents players from receiving more items than can fit on their hotbar (i.e. eight items, in addition to their main weapon). This setting is enabled by default and resembles the behavior from *Missile Wars*.

Note that players may still have more items than can fit on their hotbar if they pick up extra projectiles like **[arrows](https://zeroniaserver.github.io/RocketRidersWiki/utilities/arrows)**, as well as **[tipped arrows](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups#tipped-arrows)** and **[Tridents](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups#trident)** from **[Powerups Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups)**.

---
### Item Stacking

When enabled, players can have more than one of any item in their inventory at a time.

When disabled, they may only have multiple **[arrows](https://zeroniaserver.github.io/RocketRidersWiki/utilities/arrows)** in a stack. Similar exceptions may also be made depending on the active **[gamemode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes)** and selected **[modifiers](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers)**. For instance:

- In **[Capture the Flag Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)**, players can have up to 2 **[Canopies](https://zeroniaserver.github.io/RocketRidersWiki/utilities/canopy)** at a time.
- The **[Surprise Egg modifier](https://zeroniaserver.github.io/RocketRidersWiki/modification_roomm/modifiers#surprise-egg)** lets players receive "Surprise Eggs" that can stack up to 3.

This setting is disabled by default and resembles the behavior from *Missile Wars*.

---
### Additional Signs

Besides the above game rules, there are three additional signs in this section of the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)**:
- A sign to **Repeat Settings** for up to 4 games. This automatically closes off the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** and resets the arena when the game ends, thus preserving current game settings until the settings have been repeated the specified number of times.
- A sign to **Restore Default Game Rules**, which sets all above game rules to their indicated defaults.
- A sign to **Restore Global Defaults**, which resets the *entire* **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** to the same state as when the map is first loaded.