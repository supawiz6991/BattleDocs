---
id: getting-started
title: Getting Started
sidebar_label: Getting Started
---

# Getting File(s)

You can get the latest `jars` for BattleArena from:

- Stable - [Spigot](https://spigotmc.org)
- Stable - [BukkitDev](https://dev.bukkit.org)
- Bleeding - [Jenkins Server](https://ci.battleplugins.org)

> > Add section about Spigot / Paper builds...

# Installing

To install the BattleArena plugin on your server, follow these easy steps:

1. Download the plugin from one of the links above
2. Drag and drop the plugin into the plugins folder of the server
3. Start your server
4. Wait for the server to fully start
5. Make sure there are no errors
6. Configure the plugin
7. Once you're done configuring, run **/ba reload** to reload the plugin. If you were configuing an arena, run **/\

  <game\> reload</game\>

  **

  (e.g. **/arena reload**) to reload the arena.

# Configuring

This should be the layout of your BattleArena files:

```
/server.jars
/plugins/
/plugins/BattleArena.jar
/plugins/BattleArena/competitions
/plugins/BattleArena/messages
/plugins/BattleArena/modules
/plugins/BattleArena/otherPluginConfigs
/plugins/BattleArena/saves
/plugins/BattleArena/victoryConditions
/plugins/BattleArena/config.yml
/plugins/BattleArena/classes.yml
/plugins/BattleArena/messages.yml
/plugins/BattleArena/spawns.yml
/plugins/BattleArena/teamConfig.yml
```

Latest Config File: <https://github.com/BattlePlugins/BattleArena/blob/master/src/java/config.yml>

See these pages for more info on getting started:

1. [Config (Simple)](ba/config/simple.md)
2. [Config (Advanced)](ba/config/advanced.md)
3. [Commands](ba/config/commands.md)
4. [Permissions](ba/config/permissions.md)
5. [Debug](ba/config/debug.md)

# Getting Stats

If you would like to track statistics from arenas or games, our sister plugin [BattleTracker](bt/index.md), does all this. You can use it to view how many win, losses, streaks or elo someone has in a specific game. Some arena extensions may use BattleTracker even further and track more information based on the arena type itself. Refer to the BattleTracker page for more information.

# Setting Up your first Arena

Now that you have the plugin set up and configured, take a look at the links below for how to set up an arena!

- [Creating an Arena (Simple)](ba/arenas/simple.md)
- [Creating an Arena (Advanced)](ba/arenas/advanced.md)
