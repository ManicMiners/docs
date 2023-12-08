# Triggers
A trigger activates in response to things that happen in the world, such as a wall being drilled or a miner walking over a tile. A list of triggers can be found below. In addition there are triggers that can be used by [Classes](_pages/Classes) but since available triggers differ between classes they are not mentioned here in detail.
Triggers may be used with if and when occurrences.

|Trigger|Syntax|Description|
|----|----|----|
|built|(built:ROW,COLUMN)|Triggers when a building is built upon the specified coordinate.|
|change|(change:ROW,COLUMN|Triggers when a wall at ROW,COLUMN is changed in any way. This includes reinforcing, shoveling once, drilling, finding a cave etc.|
|change|(change:ROW,COLUMN,ID)|Triggers only if the tile is changed to the specified tile ID.|
|click|(click:ROW,COLUMN)|Triggers when the player clicks the tile at the specified coordinates. (The tile has to be visible.)|
|drill|(drill:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is drilled or collapses.|
|drive|(drive:ROW,COLUMN)|Triggers when a [Vehicle](_pages/ClassesVehicles) is driven over the specified tile.|
|drive|(drive:ROW,COLUMN, NAME)|Like drive but trigger only for the specified [Vehicle](_pages/ClassesVehicles). (Require named vehicle variable or class.)|
|enter|(enter:ROW,COLUMN)|Activates when either a [Miner](_pages/ClassesMiners) or [Vehicle](_pages/ClassesVehicles) enter a tile. This version does not trigger on creatures, only miners and vehicles.|
|enter|(enter:ROW,COLUMN,NAME)|Like enter but trigger only for the specified object or collection. This does work on creature objects and collections.|
|hover|(hover:ROW,COLUMN)|Triggers when the player hovers the tile at the specified coordinates with the mouse cursor. (The tile has to be visible.)|
|laser|(laser:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is destroyed by a laser.|
|laserhit|(laserhit:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is hit by a laser.|
|reinforce|(reinforce:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is reinforced by any unit.|
|time|(time:SECONDS)|Triggers when the specified amount of seconds have been reached. (Supports decimal floats.)|
|walk|(walk:ROW,COLUMN)|Triggers when a [Miner](_pages/ClassesMiners) walks on a tile.|
|walk|(walk:ROW,COLUMN,NAME)|Like walk but trigger only for the specified [Miner](_pages/ClassesMiners). (Require named miner variable.)|
|comparison|(`expression`)|Activates when the `expression` is evaluated as `true`. See the next section for usage.|
|CLASS||Activates when the class is interacted with in some way. See the [Classes](_pages/Classes) page for details.|

## How to monitor triggers (comparisons)
A trigger can be set to fire based on a comparison between two [Variables](_pages/Variables). This is the same as asking the game a yes/no question like *is value1 greater than value2?*. The comparison or question must evaluate to `true` for the trigger to fire. You can use this to e.g. play a sound when the player has collected half of the amount of crystals needed complete a objective.

!> All variables used within a trigger are converted to integers which cuts off any decimals. This is different from rounding as if you compare 2.2 and 2.9 they will be equal. Furthermore comparisons are not to be confused with conditions that are marked by double parenthesis `(())` although they work in a similar way.

?> The compared _values_ can be set to any valid `float`, `integer`, [Macro](_pages/Macros), [Class Macro](_pages/Classes), or regular numeric values.

|Logical operators|Meaning|
|---|---|
|>|Larger than|
|>=|Larger than or equal to|
|<|Less than|
|<=|Less than or equal to|
|==|Equal to|
|!=|Not equal to|

### Example

```mms
	int VALUE1=1
	int VALUE2=2
	
	if(VALUE1>=VALUE2)[EVENT] #Trigger1
	if(VALUE2>=VALUE1)[EVENT] #Trigger2
```

In the above code only `Trigger2` will fire as `2>=1` is `true`, but `1>=2` is `false`.
