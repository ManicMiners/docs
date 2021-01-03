# Scripting

Scripting is programmed level-specific behaviour that is currently defined by inputting command lines in the level files' script section. It has **three main components:**

* **Variables**
* **Triggers**
* **Events**

**Variables** are used to keep track of what's happening in the level. **Triggers** check for when something specific occurs in the level. **Events** are executed to alter the level or player in some way.

?> The game provide a handy log that tells you exactly what has occured and if any errors happen.

![ShowLogButton_Screenshot](_media/EditorShowLog.png "Show Log")


<img src="_media/EditorScriptingMenu.png" alt="Scripting Button" width="100" style="float:left; margin: 0.2em"/>
To assist you with scripting the Level Editor can display the Row, Column and Tile ID of the tile beneath the mouse cursor. This function is activated when you press the Script Interface button in the Level Editor.

<p style="clear:both; float:none;" />

!> If you notice something that's incorrect or require an update, create a issue on **[Github](https://github.com/ManicMiners/docs/issues)** or come over to the **#Scripting** channel over on **[Discord](https://discord.gg/85k8JHz)**.

## Links
 - [Discord](https://discord.gg/85k8JHz)
 - [Manic Miners](https://manicminers.baraklava.com/)

# Level data file
The Level data file contains all the information needed to generate a level including scripting. Among other useful things it describes the [tile ID's](https://manicminers.fandom.com/wiki/Level_data_file#Tile_ID_list:)