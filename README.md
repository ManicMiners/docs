# Scripting

Scripting is programmed map specific behavior that is currently defined by lines in the .MAP file **\[script\]** section. It has **three main components:**

- **Variables** are used to keep track of what's happening in the level.
- **Triggers** check for when something specific occurs in the level.
- **Events** are executed to alter gameplay in some way.

Variables, Triggers, and Events use [Classes](_pages/Classes) to deal with objects in the gameplay.

Combined - script may respond to changes in the map and objects and record those changes or make gameplay changes based on interactions. For example when a miner in a vehicle drives over a location, the script could revel a new area of the map to explore.

Via script, one can make significant changes to the map itself. Any tile can be turned into any other tile, allowing creation and changes to lakes, rivers, walls, spawning monsters, etc. There are a few limitations:
- no changes to tile height. Height is set at map load time.
- no new automatic undiscovered caverns may be generated.
- no new miners and buildings, only the user is able to download miners or make new buildings.
- no new landslides or erosions - they are set at map load time.

It is possible via script to dramatically affect the gameplay - one could simulate lava and water floods, destroy bases and vehicles, spawn waves of monsters, change areas of the map to create new walls and paths, change available air, and many other things. You are mainly limited by your imagination and ability to convert an idea into working script. 

Start by reviewing the [Scripting Structure](_pages/ScriptingStructure)

Reserved words are here: [Reserved Words](_pages/ReservedWords)

>The game provides a handy log that tells you exactly what has occurred and if any errors happen. Be aware that these are limited in number of events so fast timers or large scripts may exceed these limits making the debugging portion of your map more difficult. That said, scripts of tens of thousands of lines and thousands of event chains and variables do work as expected - so far no real limits have been discovered on size of script, number of event chains or variables.

![ShowLogs_Screenshot](_media/EditorScriptingOptions.png "Script Button")

![ShowLog_Screenshot](_media/EditorShowLogs.png "Show Logs")

To assist you with scripting the Level Editor can display the Row, Column and Tile ID of the tile beneath the mouse cursor. This function is activated when you press the Script Interface button in the Level Editor.

>If you notice something that's incorrect or require an update, come over to the **#Scripting** channel over on **[Discord](https://discord.gg/85k8JHz)**.

The script syntax will most likely confuse one at first - especially if one is familiar with modern free format programming languages. You cannot indent for readability - in general spaces are only allowed in a few specific places. There are no complex logical  conditions or expressions - in many ways those whom have had experience with assembly will notice many similarities.

>It is highly recommended that one review the demo scripts provided with the game to understand the syntax rules. If you are wondering if it is known how to do something - these would be the best place to start your search. These are found in the location where Manic Miners is installed in the following subdirectory path: ManicMiners\Levels\DEMO\Scripts

Additional formating rules are found in this set of documents.

## Links
 - [Manic Miners Discord](https://discord.gg/85k8JHz)
 - [Manic Miners Homepage](https://manicminers.baraklava.com/)
 - [Manic Miners Wiki](https://manicminers.fandom.com/)
