# Scripting

NOTE: If you are reading this on the main github repro - click to navigate to this documentation:  https://manicminers.github.io/docs/#/README

Manic Miner maps are text files ending in .DAT extension.

The map file is organized into sections. A complete description of each section is documented here: [DAT file format](_pages/DatFileFormat)

Scripting is programmed map specific behavior that is defined by lines in the .DAT file `script` section.

Two other sections indirectly work with the script section.
- `objectives` may refer to variables defined in the script section
- `blocks` may call EventChains in the script section or EventChains may be defined in blocks for scripts to call.

Scripts have **three main components:**

- **Variables** are used to keep track of what's happening in the level.
- **Triggers** notify when something specific occurs in the level.
- **Events** are executed to alter gameplay in some way.

Events can be combined into sequence of events called Event Chains and they are the only way for a trigger to execute multiple statements (events).

Variables, Triggers, and Events use [Classes](_pages/Classes) to deal with objects in the gameplay.

Combined - script may respond to changes in the map and objects and record those changes or make gameplay changes based on interactions. For example when a miner in a vehicle drives over a location, the script could revel a new area of the map to explore.

Via script, one can make significant changes to the map itself. Any tile can be turned into any other tile, allowing creation and changes to lakes, rivers, walls, spawning monsters, etc. There are a few limitations:
- No changes to tile height. Height is set at map load time.
- No new automatic undiscovered caverns may be generated.
- No new miners, buildings and vehicles - only the user is able to create and interact with objects.
- No new landslides or erosions - they are set at map load time.
- No movement to any unit. The only movement control script has is the ability to set a flee location for creatures.

It is possible via script to dramatically affect the map which will affect gameplay. One could simulate lava and water floods, destroy bases and vehicles, spawn waves of monsters, change areas of the map to create new walls and paths, change available air, and many other things. 

Start by reviewing the [Scripting Structure](_pages/ScriptingStructure)

Reserved words are here: [Reserved Words](_pages/ReservedWords)

>The game provides a handy log that tells you exactly what has occurred and if any errors happen. Be aware that these are limited in number of events so fast timers or large scripts may exceed these limits making the debugging portion of your map more difficult. That said, scripts of tens of thousands of lines and thousands of event chains and variables do work as expected - so far no real limits have been discovered on size of script, number of event chains or variables.

![ShowLogs_Screenshot](_media/EditorScriptingOptions.png "Script Button")

![ShowLog_Screenshot](_media/EditorShowLogs.png "Show Logs")

To assist you with scripting the Level Editor can display the Row, Column and Tile ID of the tile beneath the mouse cursor. This function is activated when you press the Script Interface button in the Level Editor.

>If you notice something that's incorrect or require an update, come over to the **#Scripting** channel over on **[Discord](https://discord.gg/85k8JHz)**.

The script syntax will most likely confuse one at first - especially if one is familiar with modern free format programming languages. You cannot indent for readability - in general spaces are only allowed in a few specific places. There are no complex logical conditions or expressions. There are no complex arithmetic operations. In many ways those whom have had experience with assembly will notice many similarities.

>It is highly recommended that one review the demo scripts provided with the game to understand the syntax rules. If you are wondering if it is known how to do something - these would be the best place to start your search. These are found in the location where Manic Miners is installed in the following subdirectory path: ManicMiners\Levels\DEMO\Scripts

Additional formatting rules are found in this set of documents.

# Undefined Behavior
The terms `non-deterministic` and `undefined` are used interchangeably in this documentation. They are both referring to either behavior or syntax that cannot be depended upon by the map developer. Basically - don't do that.

## Links
 - [Manic Miners Discord](https://discord.gg/85k8JHz)
 - [Manic Miners Homepage](https://manicminers.baraklava.com/)
 - [Manic Miners Wiki](https://manicminers.fandom.com/)
