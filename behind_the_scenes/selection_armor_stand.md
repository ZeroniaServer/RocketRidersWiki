---
layout: post
title: Selection Armor Stand
parent: Behind the Scenes
nav_order: 1
---
**Selection Armor Stand**
---

_Hey kids, here's a fun little trick to impress your friends: run `/kill @e[type=armor_stand,tag=Selection]` in chat in any **Rocket Riders** world and see what happens next!_

...okay, no. Don't. Please. I'm begging you. For some god-forsaken reason, we decided to store pretty much **ANYTHING AND EVERYTHING ROCKET RIDERS NEEDS TO FUNCTION** into one obscure, invisible armor stand in some random corner of the Lobby. You read that right.

So, suffice to say, don't kill that armor stand. Almost every important function in the **[Rocket Riders codebase](https://github.com/ZeroniaServer/RocketRiders)** is run by `@e[type=armor_stand,tag=Selection]`. Any time you see `@s`, chances are that it's referring to this armor stand (or the player or something... but probably the armor stand).

---

The magic of this system is that, by using our own scoreboard objectives and tags along with `scores=` and `tag=` target selector arguments, we can specify different states and configurations of the game based on what's stored in the Selection armor stand.

For instance, the Selection armor stand has the tag `GameStarted` whenever, you know, a game has started. Or, the tag `GameEnd` whenever the game is ending. Also, the `count` scoreboard objective is used to time the countdown before the game starts, and the `endtimer` scoreboard objective is used to time the celebration period before the players return to the lobby.

Anything to do with the **[Modification Room](https://zeroniaserver.github.io/RocketRidersWiki/modification_room)** is also directly tied to the Selection armor stand. All game configurations for **[active items](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/item_selection)**, **[base decorations](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/base_customizer)**, **[game rules](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/game_rules)**, **[modifiers](https://zeroniaserver.github.io/RocketRidersWiki/modification_room/modifiers)**, **[gamemodes](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes)**, and the like are stored there for every sign clicked.

---

There's loads of these tags and scoreboards related to the Selection armor stand scattered around the **[codebase](https://github.com/ZeroniaServer/RocketRiders)** — too many to cover without this single wiki page rivaling the Constitution in length and quite possibly boring you to death.

But, if you're ever curious about anything going on in the game, try running `/tag @e[type=armor_stand,tag=Selection] list` in chat (make sure the `sendCommandFeedback` gamerule is enabled first) and see what you can find! Also, `/scoreboard objectives setdisplay sidebar <objective>` is your best friend for anything related to scoreboards (look for the UUID `43060068-c551-4d6a-a6c8-7c5844910f65` — that's our favorite armor stand!).

We would not recommend actually setting any tags or scores yourself unless you really know what you're doing. Most of the stuff you'd ever really need to do is probably written for you in fancy little **[Operator Functions](https://zeroniaserver.github.io/RocketRidersWiki/behind_the_scenes/operator_functions)** anyway.

But if you do decide to fool around with it for yourself, _you've been warned..._

Also, again, PLEASE DON'T KILL THIS ARMOR STAND.

Seriously.