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
|drain|drain:NUM|Will drain NUM crystals. This is the same as a slimy slug draining them.|
|drill|drill:ROW,COLUMN|Drill tile ROW,COLUMN. It will play the appropriate effect and place rubble. All wall tiles can be drilled with this event including those not normally drillable. Drilling a wall may cause other tiles to automatically collapse. This event may cause drill triggers to fire.
|emerge|emerge:ROW,COLUMN,DIRECTION,COLLECTION,DISTANCE|Causes a monster to emerge. ROW,COLUMN integers are desired tile. DIRECTION is one of A,N,S,E,W. COLLECTION is one of CreatureRockMonster_C, CreatureLavaMonster_C, CreatureIceMonster_C. DISTANCE is integer distance from ROW,COLUMN to find emergeable tile to use.|
|enable|enable:COLLECTION|Enable the given object type. See description below for list of types.|
|flee|flee:OBJECT,ROW,COL|Causes the given monster object (or collection) to flee to the given tile. Once there, the Creature will try and escape as it normally does. Collections will cause all creatures of that collection to flee to that location.|
|heal|heal:OBJECT,AMOUNT|OBJECT is a miner, building or vehicle variable to heal. AMOUNT is number of hit points to give to unit. Unit cannot be healed beyond full health. Use .hp datafield to see current hit points. You cannot heal creatures!|
|hidearrow|hidearrow:ARROW|The arrow is hidden until manually shown again.|
|highlight|highlight:ROW,COLUMN,ARROW|Shows a highlight the size of a tile at ROW,COLUMN.|
|highlightarrow|highlightarrow:ROW,COLUMN,ARROW|Executes both showarrow and highlight
|kill|kill:VARIABLE|kill will transport up the given object, either building, miner, or vehicle. If object also has a .dead trigger, that trigger will fire. Does not work with collections, must be a variable based object. Does not work with creatures.|
|lose|lose:MsgStr|Player loses the level with the message defined by string MsgStr. If no string is supplied, they lose the level anyway.|
|message|msg:MsgStr|Display the message string MsgStr, as defined above. Message is added to the list of message in the message area of the user interface. You must use a string variable or a numeric value that will be displayed as a string - you cannot use a string constant.|
|pan|pan:ROW,COLUMN|The player's camera pans to the tile at ROW,COLUMN. The view direction does not change.|
|pause|pause|Pauses the game. A bit weird right now as it stops the camera lag effect. The player can unpause with the pause button (P)|
|place|place:ROW,COLUMN,ID|Place a tile with the specified [ID](_pages/LevelDataFile) in the level at the coordinates given by ROW and COLUMN.__**__|
|qmessage|qmsg:MsgStr|Display the message string MsgStr, wait for message to be acknowledged by user. You must use a string variable or a numeric value that will be displayed as a string - you cannot use a string constant.|
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

<br>__**__ If you place a wall on top of a miner or vehicle, they will just phase through the ground. This behaviour will be updated in the future to simply bury them until they are dug out.

## Unknown Events
> These are events that appear to be known by the engine but no one has figured out the syntax and behavior.

|Event|Syntax|Description|
|---|---|---|
|landslide|unknown|unknown, landslide is a reserved word.|

## Player interaction
> These events interact directly with the player and should be used with caution.

|Event|Syntax|Description|
|---|---|---|
|pause|pause|Pauses the game. When the game is paused, time does not pass, timers do not fire. The player can unpause with the pause button (P) or by unpause event.|
|reset|reset|Resets the player's selection (equivalent to a right-click)|
|resetspeed|resetspeed|Loads the game speed from settings again.|
|resume|resume|Same as unpause.|
|speed|speed:NEW_SPEED|Sets the game speed to NEW_SPEED temporarily. The speed does not save and should only be used in specific instances, like a slow motion sequence. Does not prevent the player from increasing the speed in settings.|
|unpause|unpause|Resumes the game if paused. Note that since time does not pass while the game is paused and timers are suspended - this can only be called via player interaction such as clicks.|


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
|VEHICLENAME_C|Toggle player's ability to teleport a specific vehicle class.|
|BUILDINGNAME_C|Toggle player's ability to teleport a specific building class.|
|light/lights|Toggle all ambient light in the cavern. The player cannot override this. Vehicles have floodlights that still show and some miner helmets have a light that will still show.|

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

While the engine will convert bool to int automatically - it is poor programming practice to mix bool and integers. bool should only set to true/false and only tested against true/false.

Strings only support + and += operations. The values of int and float variables are converted to strings. 

## drill and place events
There are only two ways for script to modify the map.
- drill: This event will drill a single wall. Drilling a wall may cause other walls to automatically collapse.
- place: This event replaces a tile with another Tile ID. Note that the drill event is different than the drill trigger even though they have the same name.

Since place and drill only modify a single tile - the game collects up all of the place and drill events and processes them once the calling trigger returns. This allows creation of new walls, destroying walls, changing ground, adding and removing lava and water. Basically any tile may be changed to another tile id with place.

Note that a wait event also allows processing of all queued place events. Thus one can do animations - change some tiles - wait - change more tiles - wait, etc.

The engine has a limit on the number of tiles that may be modified in the context of a trigger - that value is somewhere around 630 tiles. Non-deterministic results may happen changing too many tiles. This can be seen in the map editor where a range goes red when it is too large. Script that changes hundreds of tiles may cause a lag spike to the user and thus one may find better interactivity by limiting updates to smaller number of tiles and doing them over a time period.

Water and lava are special tiles. They require custom textures and the engine is not able to mix new water and lava tiles in the context of the same trigger. Also trying to place either water or lava tile(s) when other tiles are changed has the same limitation.  Thus in the context of a single trigger you may only place
- only water
- only lava
- only non water/lava.

Attempts to do more than one of these has non-deterministic results.  One must be aware that multiple triggers may fire around the same time and the same restrictions still apply so beware of these cases when modifying maps. Thus it is a good idea after using place to change tiles - if any of them could be water/lava, using a wait event with a short timeout is a good idea to allow the changes to be processed.

A drill event is similar to a place event, so if you use drill, you cannot also place either water or lava from the same trigger without a wait event.

You cannot use place to create new undiscovered caverns. Undiscovered caverns are only setup by the engine during map load and are fixed by the time script starts executing.
A currently undiscovered cavern may have its walls modified (for example changing from solid rock to loose rock) since you are not changing the undiscovered space.

Undiscovered caverns have ground tiles with special ID's - they are 100 greater than normal ids. Walls do not have this +100 added to them - they are walls. Once the cavern is discovered, all of the ground tiles will have the +100 removed from them.

A drill event will signal drill triggers for any wall tile that is collapsed as part of the drill event.

Both drill events and place events will signal change triggers for any tile changed by the events.

Drill and change triggers may execute at the same time as the trigger that used the drill or place events.

## Special Event Modifiers

There are two special event modifiers. These may only be used on events within an Event Chain, and were added specifically for features needed by the block system.

- Failed emerge operator `~`
- Random event from a list `?`

### Random event from a list.
Within an Event Chain, all consecutive events that start with a question mark are treated as a list of event. Only one of them will be executed, the rest will be ignored. The event chosen is at random.

Example:

```
MyChain::;
?msg:"one";    # maybe we display this message
?msg:"two";    # or this message
?msg:"three";  # or this message, but only one event will be chosen at random
```

When the Event Chain MyChain is run, only one of the three msg lines will be chosen randomly. The others will be skipped. This modifier applies to any event line including called event chains.

```
MyChain::;
?DoChain1;    # only one of these four event chains will be executed
?DoChain2;    # only one of these four event chains will be executed
?DoChain3;    # only one of these four event chains will be executed
?DoChain4;    # only one of these four event chains will be executed
```

Any event that does not start with the `?` character (or the end of the chain) will end the list, and only one of the events in the list will be executed.

### Emerge Event failed.
There is a special modifier `~` that will cause an event to be executed if the emerge event fails. In the block system, this is how the backup wires are implemented. If the emerge event was successful, the event chain containing the `~` event will be terminated.

Because a successful emerge will cause the `~` event to exit the current event chain, it is important to isolate the emerge and the `~` event from other logic.

Example:

```
bool bEmergeGood;

MyEvent::;
DoEmerge;
((bEmergeGood==true))[EmergeOk][EmergeBad];

DoEmerge::;
bEmergeGood=true;   # assume emerge will work
emerge:2,3,A,CreatureIceMonster,0;
~bEmergeGood=false;  # emerge failed

```
In the above example, either the EmergeOK or EmergeBad events will be called depending on if the emerge worked or not. By having the `~` operator on the last line of the chain, the chain will work as expected.

Example of incorrect usage:
```
MyEvent::;
emerge:2,3,A,CreatureIceMonster,0;
~msg:"Monster failed to emerge";
MoreStuff;     # incorrect, if the monster did emerge, this line is never executed
```

In the above example, the event chain MoreStuff will not execute if the emerge was successful since the ~msg line will fail and cause the event chain to end.

The main point to remember is to have the `~` event as the last event of the event chain, then the engine behavior will be as expected and your coding will be easier. This is what the block system does when it turns the backup wires into internal event chains.

You may have multiple failed events.
```
DoEmerge::;
emerge:2,3,A,CreatureIceMonster,0;
~EmergeFailed1;  # emerge failed
~EmergeFailed2;  # emerge failed.
```

Both the  `~` events will be executed if the emerge fails. If the emerge event is successful, the event chain will exit on the first `~` line.

## Collapsing Walls

In general a wall needs to be two  tiles thick. Drilling one of them, will collapse the other side except if the other side is a hidden area. Then you actually have to drill both.   If you want to make it so you only have to drill one wall for a hidden area - its very easy.  Three ways:
- Visual block system. Put a change trigger on the wall you will drill, connect with a wire to a drill event to the other wall to automatically drill. you can connect multiple wires and drill multiple parts of the wall causing larger areas to collapse.
- Script. Use a trigger:  if(drill:ROW,COL)[drill:ROW1,COL1]
Either of these will work. If you have multiple places where the wall could be drilled, have a trigger for each one that can be drilled. You will find many maps use this. It is common to call an eventchain to drill many parts of the wall, causing multiple walls or a long wall to collapse
- Editor, use flat mode and draw a single width wall. This can be confusing - it will show a squished wall tile that is only a single tile thick. The confusing part is - they only work as expected if they are enclosing an undiscovered area. Then you get a wall that is a single tile thick. But they can't be used as a wall for a discovered area. Why?  Walls need to be two tiles thick to prevent collapsing except if they are enclosing an undiscovered area. So if you use flatten mode where both sides are a discovered area - the wall will collapse at runtime.

So most walls are two tiles thick to prevent collapsing. A call can be a single tile thick if it encloses a hidden area, and once the area is discovered all single tile thick walls will collapse that are also discovered on the other side.

There is also a special cliff tile (listed as experimental in the UI) that can sort of be used in a similar way but it has its own behavior that you need play with - its really only intended to prevent objects from falling down but it also has some collapse behaviors. Normally you can't drill it but with blocks or script you can.
