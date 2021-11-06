---
layout: post
title: Vortex
parent: Utilities
nav_order: 5
---
**Vortex**
---

The **Vortex** is a floating landmine that detects and drifts towards enemy players before exploding in close proximity. It also explodes whenever:
- it is shot by an **[arrow](https://zeroniaserver.github.io/RocketRidersWiki/utilities/arrow)** or **[Nova Rocket](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)**.
- a nearby **Vortex** explodes (allowing for chain reactions).
- any other explosion occurs in a 5 block radius.
- it is occluded by a block (excluding invisible/transparent blocks like `air` as well as `nether_portal`).

It is deployed by throwing an egg, which creates a **Vortex** after 1 second of flight. Once thrown, the **Vortex** emits particles of the respective team's color and the ender pearl icon in the center spins around.

When an enemy player gets within 6 blocks of a **Vortex**, it stops spinning and turns to stare at them. If an enemy player gets within 4 blocks of the **Vortex**, it becomes "primed," at which point the icon in the center changes from an ender pearl to an eye of ender.

Once primed, the **Vortex** begins to chase any enemy players within 4 blocks of itself (at a speed of 2 m/s) and spins even faster when there are no enemy players in range. When an enemy player is within 2 blocks of the **Vortex** for half a second (nonconsecutive), it explodes. If the resultant explosion kills any players, the player who threw the **Vortex** is credited for the kill.

---
### Use Cases

A **Vortex** is most useful when thrown near enemy players, where it may drift towards those players and explode (as described above) or at least keep them at bay. It may also be thrown out in front of the player's base or other key locations near the player to ward off enemies.

If the enemy player refuses to provoke a **Vortex** themself, it may be shot with an **[arrow](https://zeroniaserver.github.io/RocketRidersWiki/utilities/arrow)** or **[Nova Rocket](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)** to explode it instead.

Since the **Vortex** explodes when occluded by a block, it may also be thrown in the path of a missile to automatically and instantly explode the missile the moment it collides with the **Vortex**.

A **Vortex** may <ins>**not**</ins> be thrown near your own portal to lose the game (in **[gamemodes](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes)** with portals, anyway). However, it *can* be thrown near the other team's portal and exploded thereafter by any means to win the game. This is unlike other utility items such as **[Nova Rockets](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)** and **[Fireballs](https://zeroniaserver.github.io/RocketRidersWiki/utilities/fireball)**, which require the **[Snipe Portals game rule](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/game_rules#snipe-portals)** (disabled by default) to be used against enemy portals.

As a projectile, the **Vortex** egg may be used to launch **[Fireballs](https://zeroniaserver.github.io/RocketRidersWiki/utilities/fireball)** similar to **[arrows](https://zeroniaserver.github.io/RocketRidersWiki/utilities/arrow)** and **[Shields](https://zeroniaserver.github.io/RocketRidersWiki/utilities/shield)**.

---
### Gamemode Specific Behavior

In **[Powerups Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups)**, players may obtain **[Tridents](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/powerups#trident)** that can also be used to shoot a **Vortex**. Note that this kills the **Trident** in the process.

In **[Chase Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/chase)**, since only Blue team is joinable and friendly fire is enabled, a **Vortex** may be used against players on the same team. It behaves practically identically to a Yellow **Vortex** (apart from the particles) in this case.

In **[Swap Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap)**, the default **Vortex** behavior is not present, and eggs are instead used as **[ICBMs](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap#icbm)** (a gamemode-exclusive utility item).

In **[Capture the Flag Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/ctf)**, a **Vortex** may not spawn in a close proximity of the flag poles. This prevents overpowered defensive strategies and never-ending games.