# Triggers
A trigger activates in response to things that happen in the world, such as a wall being drilled or a miner walking over a tile. A list of triggers can be found below. In addition there are triggers that may be used with [Classes](_pages/Classes) but since available triggers differ between classes they are not mentioned here in detail.

Triggers are used with `if` and `when` occurrences. There are a total of 6 forms for if/when triggers. The TRUEEVENT is always required. If there is a CONDITIONAL, then there is an optional FALSEVENT allowed.
```
if (TRIGGER)[TRUEEVENT]
if (TRIGGER)((CONDITIONAL))[TRUEEVENT]
if (TRIGGER)((CONDITIONAL))[TRUEEVENT][FALSEEVENT]
when (TRIGGER)[TRUEEVENT]
when (TRIGGER)((CONDITIONAL))[TRUEEVENT]
when (TRIGGER)((CONDITIONAL))[TRUEEVENT][FALSEEVENT]
```
> TRIGGER can itself be a comparison that tests macros, variables, and values.

|Trigger|Syntax|Description|
|----|----|----|
|built|(built:ROW,COLUMN)|Triggers when a building is built upon the specified coordinate.|
|change|(change:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is changed in any way. This includes reinforcing, shoveling once, drilling, finding a cave etc.|
|change|(change:ROW,COLUMN,ID)|Triggers only if the tile is changed to the specified tile ID.|
|click|(click:ROW,COLUMN)|Triggers when the player clicks the tile at the specified coordinates. (The tile has to be visible.)|
|drill|(drill:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is drilled or collapses.|
|drive|(drive:ROW,COLUMN)|Triggers when a [Vehicle](_pages/ClassesVehicles) is driven over the specified tile.|
|drive|(drive:ROW,COLUMN, NAME)|Like drive but trigger only for the specified [Vehicle](_pages/ClassesVehicles). (Require named vehicle variable or collection.)|
|enter|(enter:ROW,COLUMN)|Activates when either a [Miner](_pages/ClassesMiners) or [Vehicle](_pages/ClassesVehicles) enter a tile. This version does not trigger on creatures, only miners and vehicles.|
|enter|(enter:ROW,COLUMN,NAME)|Like enter but trigger only for the specified object or collection. This does work on creature objects and collections.|
|hover|(hover:ROW,COLUMN)|Triggers when the player hovers the tile at the specified coordinates with the mouse cursor. (The tile has to be visible.)|
|laser|(laser:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is destroyed by a laser.|
|laserhit|(laserhit:ROW,COLUMN)|Triggers when a tile at ROW,COLUMN is hit by a laser. This can be a floor tile!|
|reinforce|(reinforce:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is reinforced. Thus the tile must have been a dirt, loose rock or hard rock regular wall tile.|
|time|(time:SECONDS)|Triggers when the specified amount of game seconds have been reached since the map started. (Supports decimal floats.)|
|walk|(walk:ROW,COLUMN)|Triggers when a [Miner](_pages/ClassesMiners) walks on a tile.|
|walk|(walk:ROW,COLUMN,NAME)|Like walk but trigger only for the specified [Miner](_pages/ClassesMiners). (Require named miner variable.)|
|comparison|(`expression`)|Activates when the `expression` is evaluated as `true`. See the next section for usage.|
|CLASS||Activates when the class is interacted with in some way. See the [Classes](_pages/Classes) page for details.|

## Class specific data field triggers.
Some classes have data members that may be used as a trigger. See each class for the list of trigger data fields specific for that class.

## Comparison triggers
A trigger can be set to fire based on a comparison between two [Variables](_pages/Variables) or  macros / properties of some classes or literal values.   If the result of the comparison is true, the trigger is considered fired and then will either call the true or false event depending on the conditional.

> All variables used within a trigger are converted to integers which cuts off any decimals. This is different from rounding as if you compare 2.2 and 2.9 they will be equal. Furthermore comparisons are not to be confused with conditionals that are marked by double parenthesis `(())` although they work in a similar way.

> The compared _values_ can be any valid `float`, `integer`, [Macro](_pages/Macros), [Class Macro](_pages/Classes), or regular numeric values.

See [Conditions](_pages/Conditions) for more detail.


## Conditional triggers (comparisons)
A trigger may optionally be tested again a conditional that is either true or false. If it evaluates to `true` will cause the TRUEEVENT to fire. If the comparison is false and there is the optional FALSEEVENT, the FALSEEVENT will fire.  This test is the same as a comparison event.


## Multiple Identical Triggers
Having the same trigger type on the same tile multiple times causes undefined behavior. Example:

```
when(enter:4,5)[foo]
when(enter:4,5)[bar]
if(enter:4,5)[singleShot]
```

The same trigger is duplicated, one trigger wants to call foo event chain, another trigger wants to call bar event chain, and another trigger wants to call singleShot a single time only. Multiple triggers of the same type on the same tile cause undefined behavior in the script engine and should always be avoided.

The behavior for multiple different triggers on the same tile is not documented. Developers should not count on any specific order that triggers may fire, and using the same tile for multiple triggers will require testing to ensure it works.

## time:
There is a known exception to the no duplicated triggers rule. The engine does support multiple `time:` triggers. Each will be called in the given number of seconds after map play has started, after the `init` event chain has been called.

```
if(time:0)[startup1]
if(time:0)[startup2]
if(time:0)[startup3]
```
The three event chains startup1, startup2, startup3 will all be called at the beginning of map play right after the `init` event chain has been called.

>Avoid using `when` with time triggers. They are evaluated on every engine tick and once the given number of seconds has past, will constantly fire. Very similar to tick event chain in terms of overhead.

### Examples

```mms
	int VALUE1=1
	int VALUE2=2
	
	if(VALUE1>=VALUE2)[EVENT] # Trigger1
	if(VALUE2>=VALUE1)[EVENT] # Trigger2
```

In the above code only `Trigger2` will fire as `2>=1` is `true`, but `1>=2` is `false`.

Remember - `if` triggers only fire a single time. Once the trigger condition is met, the trigger will never fire again. `When` triggers will fire every time that condition is met.

`When` triggers may cause poor performance and undesired behavior if misused.  Lets take an example of a map where if a unit enters a given tile, it will cause a rock monster to spawn. One way to code this up would be:

```mms
string msgMonSpawn="Your presence has spawned a monster!"

when(enter:25,27)[SpawnMonster]

SpawnMonster::;
emerge:30,31,A,CreatureRockMonster_C,10;  # random spawn from any tile around 30,31 for 10 tiles
msg:msgMonSpawn;	                  # tell user its their fault
```

This will work, but it has some issues with scalability. Lets say the player makes 200 miners (yes - you can do that), and they are all grouped up, and the player sends them all to a location that just happens to cross the 25,27 tile.  This will massively lag the game as 200 triggers fire, each spawning a rockmonster and displaying 200 messages - and now the player has 200 rock monsters. Due to lag the player may not even be able to deal with it or weaker machines might just lock up.

As a map designer you have to consider that players have freedom in how they play the map and it is your responsibility to ensure your scripting does not prevent the user from playing the map.

In the above case, clearly you do not want to spawn 200 monsters. So now you have to think about - what is reasonable? Maybe only spawn a monster every 5 seconds. Once a unit enters the tile, save the time, and ignore the trigger until enough time has passed.  Here is a version that does exactly that - it is like above but with just a few changes.

```mms
string msgMonSpawn="Your presence has spawned a monster!"
float lastspawn=0        # remember last time we spawned a monster
float ftemp=0            # temp value to compute time since last spawn
int OneAtAtime=0         # flag to prevent trigger from calling recursively

when(enter:25,27)[SpawnMonster]

SpawnMonster::((OneAtAtime=1))[return][OneAtAtime=1];   # just one trigger at a time
ftemp=time-lastspawn;                     # how long since last spawn
((ftemp>=5))DoSpawnMonster;               # more than 5 seconds, spawn
OneAtAtime=0;                             # done, allow calls

DoSpawnMonster::lastspawn=time;           # save time for this spawn
emerge:30,31,A,CreatureRockMonster_C,10;  # random spawn from any tile around 30,31 for 10 tiles
msg:msgMonSpawn;                          # tell user its their fault
```
In the above case if 200 miners all cross the tile at the same time, only a single monster will be spawned even though the when trigger will fire 200 times. The eventchain SpawnMonster will simply return if it is in the middle of processing a prior call and it will only spawn a monster if one has not been spawned for 5 seconds.
