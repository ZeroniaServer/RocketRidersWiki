---
layout: post
title: Update Guide
permalink: /update_guide/
nav_order: 1
---
# **Update Guide**
---

If you have an existing Rocket Riders world that you would like to update to the latest version while still keeping your player/world data, read below (or alternatively, **[watch this video!](https://www.youtube.com/watch?v=jqhpZxDhhEs)**).

This process involves copying over the new datapack folders from the **[Rocket Riders GitHub repository](https://github.com/ZeroniaServer/RocketRiders)**.

You will need to go to the **[releases page](https://github.com/ZeroniaServer/RocketRiders/releases)** and download the Source Code zip file for the latest release.

Then drag this file to your Rocket Riders world save folder, typically located in the following places depending on your operating system:
- Windows: `%APPDATA%\.minecraft\saves\Rocket Riders`
- macOS: `~/Library/Application Support/minecraft/saves/Rocket Riders`
- Linux: `~/.minecraft/saves/Rocket Riders`

Extract the zip file and then copy everything except `empty_advancements.zip`, `LICENSE.txt`, and `README.md`, as these files should not change.

Navigate to your world's `datapacks` folder and delete the same folders you just copied from there before pasting the new ones in. Then delete the extracted folder and corresponding zip file now that you've pasted the new datapacks in.

Finally, run `/reload` ingame to load in the new datapacks! (Alternatively, close and reopen your world.) All of your world data should be saved, and the code should be fully up to date.

Note: for updating to **Version 1.1.0+**, you will need to run the command `/function rr_crusade:install` in chat in order to play **[Crusade Mode](https://zeroniaserver.github.io/RocketRidersWiki/gamemodes/crusade)**. You may also need to run `/datapack enable "file/rr_crusade"` if the first command fails.