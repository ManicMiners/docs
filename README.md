# Scripting

Scripting is programmed level-specific behavior that is currently defined by inputting command lines in the level files' script section. It has **three main components:**

- **Variables**
- **Triggers**
- **Events**

**Variables** are used to keep track of what's happening in the level. **Triggers** check for when something specific occurs in the level. **Events** are executed to alter the level or player in some way.

Start by reviewing the [Scripting Structure](_pages/ScriptingStructure)

Reserved words are here: [Reserved Words](_pages/ReservedWords)

?> The game provide a handy log that tells you exactly what has occurred and if any errors happen.

![ShowLogButton_Screenshot](_media/EditorScriptingOptions.png "Script Button")

![ShowLogButton1_Screenshot](_media/EditorShowLog.png "Show Logs")

To assist you with scripting the Level Editor can display the Row, Column and Tile ID of the tile beneath the mouse cursor. This function is activated when you press the Script Interface button in the Level Editor.

<p style="clear:both; float:none;" />

!> If you notice something that's incorrect or require an update, come over to the **#Scripting** channel over on **[Discord](https://discord.gg/85k8JHz)**.

The script syntax will most likely confuse one at first - especially if one is familiar with modern free format programming languages. You cannot indent for readability - in general spaces are only allowed in a few specific places. There are no complex logical  conditions or expressions - in many ways those whom have had experience with assembly will notice many similarities.

It is highly recommended that one review the demo scripts provided with the game to understand the syntax rules. If you are wondering if it is known how to do something - these would be the best place to start your search. These are found in the location where Manic Miners is installed in the following subdirectory path: ManicMiners\Levels\DEMO\Scripts

Additional formating rules are found in this set of documents.

## Links
 - [Manic Miners Discord](https://discord.gg/85k8JHz)
 - [Manic Miners Homepage](https://manicminers.baraklava.com/)
 - [Manic Miners Wiki](https://manicminers.fandom.com/)
