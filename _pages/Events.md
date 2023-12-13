# Predefined Event Chains

There are two predefined [Event Chain](_pages/EventChains) that you may used in your script.
- init::
- tick::

init is called at the start of the map before any other trigger. It allows you do complete whatever initialization is necessary for your map.

tick is called on every frame update. This can be as high as 350 times a seconds and it is not recommend for use.

# Events
Events describe to the game what you want it to do when a trigger is activated. Events can be placed as the true or false events on a trigger or they can be combined into an event chain.

|Event|Syntax|Description|
|---|---|---|
|addrandomspawn|addrandomspawn:COLLECTION,MINTIME,MAXTIME|Configure random spawn of a creature collection. MINTIME and MAXTIME define a random time in float seconds between each spawn wave.|
|disable|disable:COLLECTION|Disable the given object type. See description below for list of types|
|drill|drill:ROW,COLUMN|Drill tile ROW,COLUMN. It will play the appropriate effect and place rubble, ignoring what tile it is.*|
|emerge|emerge:ROW,COLUMN,DIRECTION,COLLECTION,DISTANCE|Causes a monster to emerge. ROW,COLUMN integers are desired tile. DIRECTION is one of A,N,S,E,W. COLLECTION is one of CreatureRockMonster_C, CreatureLavaMonster_C, CreatureIceMonster_C. DISTANCE is integer distance from ROW,COLUMN to find emergeable tile to use.|
|enable|enable:COLLECTION|Enable the given object type. See description below for list of types.|
|flee|flee:OBJECT,ROW,COL|Causes the given monster object (or collection) to flee to the given tile. Once there, the Creature will try and escape as it normally does. Collections will cause all creatures of that collection to flee to that location.|
|heal|heal:OBJECT,AMOUNT|OBJECT is a miner, building or vehicle variable to heal. AMOUNT is number of hit points to give to unit. Unit cannot be healed beyond full health. Use .hp datafield to see current hit points. You cannot heal creatures!|
|hidearrow|hidearrow:ARROW|The arrow is hidden until manually shown again.|
|highlight|highlight:ROW,COLUMN,ARROW|Shows a highlight the size of a tile at ROW,COLUMN.|
|highlightarrow|highlightarrow:ROW,COLUMN,ARROW|Executes both showarrow and highlight at |kill|kill:VARIABLE|kill will transport up the given object, either building, miner, or vehicle. If object also has a .dead trigger, that trigger will fire.|
|lose|lose:MsgStr|Player loses the level with the message defined by string MsgStr. If no string is supplied, they lose the level anyway.|
|message|msg:MsgStr|Display the message string MsgStr, as defined above. Message is added to the list of message in the message area of the user interface.|
|pan|pan:ROW,COLUMN|The player's camera pans to the tile at ROW,COLUMN. The view direction does not change.|
|pause|pause|Pauses the game. A bit weird right now as it stops the camera lag effect. The player can unpause with the pause button (P)|
|place|place:ROW,COLUMN,ID|Place a tile with the specified [ID](_pages/LevelDataFile) in the level at the coordinates given by ROW and COLUMN.__**__|
|qmessage|qmsg:MsgStr|Display the message string MsgStr, wait for message to be acknowledged by user|
|save|[save:MINERVAR]|Saves the last miner unit who activated a trigger into a variable.|
|savebuilding|savebuilding:BUILDINGVAR|Saves the last building that activated a trigger into given building variable.|
|savecreature|savecreature:CREATUREVARIABLE|Save last creature that activated a trigger into a creature variable.|
|savevehicle|savevehicle:VEHICLEVAR|Saves the last vehicle that activated a trigger into given vehicle variable.|
|shake|shake:VALUE|The player's camera shakes with the float VALUE. The magnitude has no limit.|
|showarrow|showarrow:ROW,COLUMN,ARROW|Shows the designated arrow at the tile ROW,COLUMN.|
|sound|sound:MySoundName|Plays the .ogg file of that name from /ManicMiners/Levels/ASSETS/Sounds (do <B>not</b> include the ".ogg" extension in the script)|
|spawncap|spawncap:Collection,MIN,MAX|For the given collection, random spawns will occur until total number of active creatures is over a random value between MIN and MAX.|
|spawnwave|spawnwave:Collection,MIN,MAX|For the given collection each spawn wave will have a random number of creatures between MIN and MAX.|
|speed|speed:NEW_SPEED|Sets the game speed to NEW_SPEED temporarily. The speed does not save and should only be used in specific instances, like a slow motion sequence. Does not prevent the player from increasing the speed in settings.|
|startrandomspawn|startrandomspawn:Collection|Start the random spawn for the given collection.|
|starttimer|starttimer:name|name is timer variable, its timer is started if it was stopped.|
|stoprandomspawn|stoprandomspawn:Collection|Stop the random spawn for the given collection|
|stoptimer|stoptimer:name|name is a timer variable, its timer is stopped if it is running.|
|truewait|truewait:REAL_SECONDS|Ask the game to wait the given float number of seconds before executing the next command. Only supported within a event chain. Does not scale with game speed. Similar to wait, be careful of reentrant events.|
|unpause|unpause|Resumes the game if paused.|
|wait|wait:GAME_SECONDS|Ask the game to wait a set amount of seconds before executing the next command. Only supported within an event chain. Scales with game speed. While waiting the engine continues to run and script responds to events - so it is possible to re-entrant into the waiting event. You are responsible for handling this case.|
|win|win:MsgStr|Player wins the level with the message defined by string MsgStr. If no string is supplied, they win the level anyway.|


?> __*__ Drilling will get fixed later to check that the tile can actually be drilled. <br>__**__ If you place a wall on top of a miner or vehicle, they will just phase through the ground. This behaviour will be updated in the future to simply bury them until they are dug out.

## Player interaction
!> These events interact directly with the player and should be used with caution.

|Event|Syntax|Description|
|---|---|---|
|pause|pause|Pauses the game. A bit weird right now as it stops the camera lag effect. The player can unpause with the pause button (P)|
|reset|reset|Resets the player's selection (equivalent to a right-click)|
|resetspeed|resetspeed|Loads the game speed from settings again.|
|resume|resume|Same as unpause.|
|speed|speed:NEW_SPEED|Sets the game speed to NEW_SPEED temporarily. The speed does not save and should only be used in specific instances, like a slow motion sequence. Does not prevent the player from increasing the speed in settings.|
|unpause|unpause|Resumes the game if paused. Note that since time does not pass while the game is paused, even with truewait, this can only be called via player interaction such as clicks.|

## Arrow events
Arrows are used for highlighting things in the world. Once you declare an arrow as a variable you can use these to move it around or hide it. The arrows have two usable components: A physical, hovering arrow, and a tile-sized highlight.

|Event|Syntax|Description|
|---|---|---|
|hidearrow|hidearrow:ARROW|The arrow is hidden until manually shown again.|
|highlight|highlight:ROW,COLUMN,ARROW|Shows a highlight the size of a tile at ROW,COLUMN.|
|highlightarrow|highlightarrow:ROW,COLUMN,ARROW|Executes both showarrow and highlight at once.|
|showarrow|showarrow:ROW,COLUMN,ARROW|Shows the designated arrow at the tile ROW,COLUMN.|

It is highly recommended to review the Arrow examples in ManicMiners\Levels\DEMO\Scripts

## Disable/Enable events
Disable/Enable is used to control what the player can and cannot do in the current level. One example might be that you don't want the player to use flying vehicles, in which case you can disable the Tunnel Scout and Tunnel Transport manually. The syntax looks like this:
```mms
disable:COLLECTION
enable::COLLECTION
```
where COLLECTION can be one of the following:

|Collection|Description|
|---|---|
|miners|Toggle player's ability to teleport miners.|
|vehicles|Toggle player's ability to teleport vehicles.|
|buildings|Toggle player's ability to teleport buildings.|
|VEHICLE_NAME_C|Toggle player's ability to teleport a specific vehicle class.|
|BUILDING_NAME_C|Toggle player's ability to teleport a specific building class.|
|light/lights|Toggle all ambient light in the cavern. The player cannot override this. Vehicles have floodlights and some miner helmets have a light.|

Example - this event chain will turn off any ability to transport miners, vehicles, buildings or use explosives:

```mms
TurnStuffOff::;
disable:vehicles;
disable:miners;
disable:buildings;
disable:Dynamite_C;
```

## Math events
Variable-types int, float and string have specific events that makes it possible to alter them while the game is running. This also work with some macros.


|Mathematical operator|Meaning|Example|
|---|---|---|
|+|Addition|a=b+c|
|+=|Addition by|a+=b|
|-|Subtraction|a=b-c|
|-=|Subtraction by|a-=b| 
|*|Multiplication|a=b*c|
|*=|Multiplication by|a*=b|
|//|Division (double forward slash)|a=b//c|
|/=|Division by|a/=b|

Math events are complete events thus you cannot use math operators inside of a conditional. You must compute the math result saving into a variable and use that variable in conditionals.

You cannot combine multiple math operators. Only a single math operation at a time - there is no support for complex operations or ordering.

While the engine will convert bool to int automatically - it is poor programming practice to mix bool and integers. Bools should only set to true/false and only tested against true/false.

Strings only support + and += operations. The values of int and float variables are converted to strings. 

## drill and place events
There are only two ways for script to modify the map.
- drill: This event will drill a single wall. Drilling a wall may cause other walls to automatically collapse.
- place: This event replaces a tile with another Tile ID. Note that the drill event is different than the drill trigger even though they have the same name.

Since place and drill only modify a single tile - the game collects up all of the place and drill events and processes them once the calling trigger returns. This allows creation of new walls, destroying walls, changing ground, adding and removing lava and water. Basically any tile may be changed to another tile id with place.

Note that a wait event also allows processing of all queued place events. Thus one can do animations - change some tiles - wait - change more tiles - wait, etc.

The engine has a limit on the number of tiles that may be modified in the context of a trigger - that value is somewhere around 630 tiles. Non-deterministic results may happen changing too many tiles. This can be seen in the map editor where a range goes red when it is too large.

Water and lava are special tiles. They require custom textures and the engine is not able to mix new water and lava tiles in the context of the same trigger. Also trying to place either water or lava tile(s) when other tiles are changed has the same limitation.  Thus in the context of a single trigger you may only place
- only water
- only lava
- only non water/lava.

Attempts to do more than one of these has non-deterministic results.

A drill event is similar to a place event, so if you use drill, you cannot also place either water or lava from the same trigger.

You cannot use place to create new undiscovered caverns. Undiscovered caverns are only setup by the engine during map load and are fixed by the time script starts executing.
A currently undiscovered cavern may have its walls modified (for example changing from solid rock to loose rock) since you are not changing the undiscovered space.

Undiscovered caverns have ground tiles with special ID's - they are 100 greater than normal ids. Walls do not have this +100 added to them - they are walls. Once the cavern is discovered, all of the ground tiles will have the +100 removed from them.

A drill event will signal drill triggers for any wall tile that is collapsed as part of the drill event.

Both drill events and place events will signal change triggers for any tile changed by the events.

Drill and change triggers may execute at the same time as the trigger that used the drill or place events.

