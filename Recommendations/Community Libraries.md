# Community Libraries

The Minescript community has created several libraries to aid you in script development.

Want to be featured here? Publish your library in #Shared-Scripts in the discord for it to be used by others!

Ideally, these submissions include a *named file*, being standard code that *is able to just be downloaded and used without any further renaming/configurations (other than those the script itself does)*. GitHub pages are preferable.


# General

## Minescript Plus

As of `18/2/2026`,

Minescript Plus is an all-purpose library that contains many helper-functions.

Its functions are split into classes, meaning that to reference something, you have to do:

```py
from minescript_plus import Util
echo(Util.get_clipboard())
```

Disclaimer: `Requires \install_mappings`, `Lib_NBT needed if using item manipulation`

Currently Supports: Python Only

Versions: 1.21.6-1.21.10 ([Standard](https://github.com/R4z0rX/minescript-scripts/blob/main/Minescript-Plus/minescript_plus.py))

Versions 1.21.5- ([legacy](https://github.com/R4z0rX/minescript-scripts/blob/e3080ad8e0ececa7c4278f525f9dbf2f9d943dc2/Minescript-Plus/minescript_plus.py))

# Items

## Lib NBT

As of `18/2/2026`,

Lib NBT is an official library created by @maxuser, one of the creators of minescript.

It offers NBT parsing, turning the strings into usable JSON dictionaries.


Disclaimer: `NBT data is currently getting phased out in favor of tags in newer minecraft versions`

Currently Supports: Python Only

Versions: 1.21.10- ([Minescript Site](https://minescript.net/downloads))

## Lib Inv

## Minescript Plus

(see above)

# BlockPack

## Lib BlockPack Parser

As of `18/2/2026`,

Lib BlockPack Parser is an official library created by @maxuser, one of the creators of minescript.

It allows python scripts to read `BlockPack` data created by many commands that get an area of blocks, as well as TNT explosions.

An equivalent to this is built into Pyjinn.

Currently Supports: Python Only

Versions: all ([Minescript Site](https://minescript.net/downloads))

# Rotation

## Rotation.py

(not added yet)

## Looker

## 

# Pathfinding - A*

A* pathfinders use the minecraft grid to pathfind, avoiding obstacles.

Currently, most A* pathfinders do not have good edge-case detection (Ex: navigating your base) but can move through open areas and mazes perfectly fine.

A* generates longer and slower paths than Theta*.


# Pathfinding - Theta*
Theta* pathfinders are similar to A*, except with the major difference being that they try to reduce the number of turns by removing nodes.

Currently, most Theta* pathfinders developed are less reliable than A*, especially on hilly terrain.

For more regular terrain, these pathfinders are much faster and more human.

# Theta*

## ThetaStar 

ThetaStar is a pathfinding script developped by @hyshenn, allowing you to pathfind to specific points in your world.

```py
from your_script import path_walk_to

target_position = (100, 65, 200)
path_walk_to(goal=target_position)
```

Disclaimer: `Requires rotation.py (see above)`

Currently Supports: Python only

Versions: all ([GitHub](https://github.com/hyshenn/thetaSTAR))

## MS Extras

MS Extras is another Theta* interface by @hyshenn, although this time using an actual minecraft mod to speed it up.

[Code Snippet](https://discord.com/channels/930220988472389713/1472882398235725908)

Disclaimer: `Requires mod from modrinth`

Currently Supports: Pyjinn & Python (Embed the pyjinn yourself if using python)

Versions: 1.21.11 CONFIRMED, likely will work with other versions. ([modrinth](https://modrinth.com/mod/ms-extras))

# World Rendering



## lib_ren

Lib Ren is a rendering library made by @JulianisLost, with compatibility up to 1.21.8.

It requires you to define each item `on_render`, so pyjinn is required, although it allows complete control over your rendering.

Disclaimer: `Requires \install_mappings`,

## Minescript Plus

Currently has limited support for abstract boxes & lines. Cannot update too many objects at one time.

(see above)

# GUI

## UI Container



## Minescript Plus

(see above)

