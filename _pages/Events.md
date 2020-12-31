# Events
Events describe to the game what you want it to do when a trigger is activated.

|Event|Syntax|Description|
|---|---|---|
|init|init::EVENT;|Creates a [[Scripting#Event Chains|event chain ]]that is called at start before any trigger in the level.|
|drill|[drill:ROW,COLUMN]|Drill tile ROW,COLUMN. It will play the appropriate effect and place rubble, ignoring what tile it is.*|
|message|[msg:MsgStr]|Display the message string MsgStr, as defined above.|
|place|[place:ROW,COLUMN,ID]|Place tile with ID at ROW,COLUMN. You can find IDs of the tiles [https://manicminers.fandom.com/wiki/Level_data_file#Tile_ID_list: here].**|
|wait|[wait:GAME_SECONDS]|Ask the game to wait a set amount of seconds before executing the next command. Only supported within an event chain. Scales with game speed.|
|truewait|[truewait:REAL_SECONDS]|Ask the game to wait a set amount of seconds before executing the next command. Only supported within a event chain. Does not scale with game speed.|
|win|[win:MsgStr]|Player wins the level with the message defined by string MsgStr. If no string is supplied, they win the level anyway.|
|lose|[lose:MsgStr]|Player loses the level with the message defined by string MsgStr. If no string is supplied, they lose the level anyway.|
|sound|[sound:MySoundName]|Plays the .ogg file of that name from /ManicMiners/Levels/ASSETS/Sounds (do '''not''' include the ".ogg" extension in the script)|
|pan|[pan:ROW,COLUMN]|The player's camera pans to the tile at ROW,COLUMN|
|shake|[shake:1.0]|The player's camera shakes with magnitude 1.0. The magnitude has no limit.|
|save|[save:SomeUnitVariable]|Saves the last unit who activated a trigger into a variable. Can be combined with walk/drive/enter triggers for example.|

*Drilling will get fixed later to check that the tile can actually be drilled.

**If you place a wall on top of a miner or vehicle, they will just phase through the ground. This behaviour will be updated in the future to simply bury them until they are dug out.

## Player interaction
<span style="color:#FF0000">'''These events interact directly with the player and should be used with caution'''.</span>

|Event|Syntax|Description|
|---|---|---|
|reset|[reset]|Resets the player's selection (equivalent to a right-click)|
|pause|[pause]|Pauses the game. A bit weird right now as it stops the camera lag effect. The player can unpause with the pause button (P)|
|unpause/resume|[unpause]/[resume]|Resumes the game if paused. Note that since time does not pass while the game is paused, even with truewait, this can only be called via player interaction such as clicks.|
|speed|[speed:NEW_SPEED]|Sets the game speed to NEW_SPEED temporarily. The speed does not save and should only be used in specific instances, like a slow motion sequence. Does not prevent the player from increasing the speed in settings.|
|resetspeed|[resetspeed]|Loads the game speed from settings again.|

## Arrow events
Arrows are used for highlighting things in the world. Once you declare an arrow as a variable you can use these to move it around or hide it. The arrows have two usable components: A physical, hovering arrow, and a tile-sized highlight.

|Event|Syntax|Description|
|---|---|---|
|showarrow|[showarrow:ROW,COLUMN,ARROW]|Shows the designated arrow at the tile ROW,COLUMN.|
|highlight|[highlight:ROW,COLUMN,ARROW]|Shows a highlight the size of a tile at ROW,COLUMN.|
|highlightarrow|[highlightarrow:ROW,COLUMN,ARROW]|Executes both showarrow and highlight at once.|
|hidearrow|[hidearrow:ARROW]|The arrow is hidden until manually shown again.|

## Disable/Enable events
Disable/Enable is used to control what the player can and cannot do in the current level. One example might be that you don't want the player to use flying vehicles, in which case you can disable the Tunnel Scout and Tunnel Transport manually. The syntax looks like this:
 disable:MACRO
where MACRO can be one of the following:

|Macro name|Description|
|---|---|---|
|miners|Toggle player's ability to teleport miners|
|vehicles|Toggle player's ability to teleport vehicles|
|buildings|Toggle player's ability to teleport buildings|
|VEHICLE_NAME_C|Toggle player's ability to teleport a vehicle of a specific [[Classes|type]]|
|BUILDING_NAME_C|Toggle player's ability to teleport a building of a specific [[Classes|type]]|
|light/lights|Disable all ambient light in the cavern. The player cannot override this. Please be mindful that right now, only vehicles have floodlights, so designing a level around it might not be very mindful. More light mechanics are coming.|

## Math events
Variable-types integer, float, string and boolean have specific events that makes it possible to alter them while the game is running. This also work with some macros.


|Mathematical operator|Meaning|
|---|---|
|+|Addition
|+=|Addition by
|-|Subtraction
|-=|Subtraction by
|*|Multiplication
|*=|Multiplication by
|//|Division (note the double lines)
|/=|Division by
