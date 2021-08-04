---
layout: post
title: Canopy
parent: Utilities
nav_order: 7
---
**Canopy**
---

The **Canopy** is a flat 7x7 platform of leaves with two logs in the middle that can be deployed via ender pearls.

---
### Deployment
When the player throws an ender pearl, it transforms into a **Canopy** after 10 ticks of uninterrupted flight.

If the ender pearl hits an obstacle before this time has elapsed, then no **Canopy** spawns and the usual ender pearl teleport behavior takes over.

If the player dies before the **Canopy** fully spawns, they are not teleported back onto it. Also, if the player dies while their ender pearl is in midair, the ender pearl dies as well (this is vanilla Minecraft behavior).

When thrown near the player's own base, the **Canopy** "quick deploys," fully constructing itself in roughly a third of the time. Otherwise, the player is frozen in place for 2 seconds and continuously teleported on top of the **Canopy** while it animates the leaves growing from the central log.

---
### Duration and Counters
Once fully deployed, the **Canopy** remains alive for 20 seconds until the logs break automatically, after which point the leaves rapidly decay (the `randomTickSpeed` gamerule is set to 25).

A **Canopy** may expire before the full 20 seconds have elapsed if one of the logs is broken by hand, replaced by another structure, or exploded. Also, if an enemy **[Nova Rocket](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)** is launched at the **Canopy**, it instantly explodes and is almost guaranteed to kill the player on top.

A **Canopy** may also be "fire-poofed," which sets all of the leaves on fire and destroys the central logs, thus killing the **Canopy**. This occurs under the following conditions:
- A **[Fireball](https://zeroniaserver.github.io/RocketRidersWiki/utilities/fireball)** is shot at or near the logs
- A flame **[arrow](https://zeroniaserver.github.io/RocketRidersWiki/utilities/arrows)** lands directly near the logs
- Fire spreads to the logs by other means (note that **Fireballs** and flame **arrows** set any leaves they contact on fire).
- A player on fire stands near the logs for a maximum of 4 seconds (known as "Canopy smoking").
- TNT explodes in a 7 block radius of the **Canopy**.

The **Canopy** duration can also be extended by 10 seconds if water from a **[Splash](https://zeroniaserver.github.io/RocketRidersWiki/utilities/splash)** falls on top of it. This is known as "Canopy watering."

---
### Use Cases

The **Canopy** is most useful to give players a chance to save themselves from certain death or gain significant vertical/horizontal distance.

Throwing a **Canopy** directly upwards gives players height advantages, which are very valuable in a game where all the **[missiles](https://zeroniaserver.github.io/RocketRidersWiki/missiles)** spawn with a downwards offset.

Also, throwing the **Canopy** downwards gives players low-ground riding opportunities, putting enemies at a disadvantage since they would incur fall damage if they try to jump down. (Note that this can be mitigated in several ways, such as landing on slime blocks and throwing **[Splashes](https://zeroniaserver.github.io/RocketRidersWiki/utilities/splash)**, or fully removed with the **[No Fall modifier](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers#no-fall)**.)

Throwing the **Canopy** off-sides (adjacent to the bases) puts players in a position where **missiles** usually cannot directly reach them, again affording some strategic advantages.

**Canopies** are especially useful when you have already been hit by a **[Nova Rocket](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)**, which propels you into the air and would normally result in certain death. Combined with the height the **Nova Rocket** gives you, you can get some immense vertical distance from a single **Canopy** throw.

Any benefits that the **Canopy** affords in this manner do come with significant drawbacks, however, due to the sheer number of counters that other **[utilities](https://zeroniaserver.github.io/RocketRidersWiki/utilities/)** can have against them (the **Nova Rocket** chiefly among them).

**Canopies** <ins>**cannot**</ins> be used to break portals. They also cannot be spawned in a 7-block radius of either team's spawnpoint.

---
### Gamemode Specific Behaviors

**Canopies** can be exploded by **[Nova Rockets](https://zeroniaserver.github.io/RocketRidersWiki/utilities/nova_rocket)** from the player's same team in **[Chase Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/chase)**, since only Blue team is joinable and friendly fire is enabled.

The **Canopy** is not obtainable in **[Swap Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/swap)**, as the items are so overpowered already that it need not exist.

The **Canopy** is not obtainable in **[1v1 Duel Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/duel)**, as it too heavily alters the normal *Missile Wars* gameplay meta so as to make ranked-style 1v1 matches less competitive.