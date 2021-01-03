# Triggers
A trigger activates in response to things that happen in the world, such as a wall being drilled or a miner walking over a tile. 

|Trigger|Syntax|Description|
|----|----|----|
|drill|(drill:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is drilled or collapses.|
|built|(built:ROW,COLUMN)|Triggers when a building is built upon the specified coordinate.|
|laser|(laser:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is destroyed by a laser.|
|laserhit|(laserhit:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is hit by a laser.|
|change|(change:ROW,COLUMN|Triggers when a wall at ROW,COLUMN is changed in any way. This includes reinforcing, shoveling once, drilling, finding a cave etc.|
|change|(change:ROW,COLUMN,ID)|Triggers only if the tile is changed to the specified tile ID.|
|reinforce|(reinforce:ROW,COLUMN)|Triggers when a wall at ROW,COLUMN is reinforced by any unit.|
|time|(time:SECONDS)|Triggers when the specified amount of seconds have been reached. (Supports decimal floats.)|
|hover|(hover:ROW,COLUMN)|Triggers when the player hovers the tile at the specified coordinates with the mouse cursor. (The tile has to be visible.)|
|click|(click:ROW,COLUMN)|Triggers when the player clicks the tile at the specified coordinates. (The tile has to be visible.)|
|walk|(walk:ROW,COLUMN)|Triggers when a [Miner](_pages/ClassesMiners) walks on a tile.|
|walk|(walk:ROW,COLUMN, NAME)|Like walk but trigger only for the specified [Miner](_pages/ClassesMiners). (Require named miner variable.)|
|drive|(drive:ROW,COLUMN)|Triggers when a [Vehicle](_pages/ClassesVehicles) is driven over the specified tile.|
|drive|(drive:ROW,COLUMN, NAME)|Like drive but trigger only for the specified [Vehicle](_pages/ClassesVehicles). (Require named vehicle variable or class.)|
|enter|(enter:ROW,COLUMN)|Activates when either a [Miner](_pages/ClassesMiners) or [Vehicle](_pages/ClassesVehicles) enter a tile.|
|enter|(enter:ROW,COLUMN, NAME)|Like enter but trigger only for the specified vehicle class or named [Miner](_pages/ClassesMiners)/[Vehicle](_pages/ClassesVehicles).|
|comparison|(`expression`)|Activates when the `expression` is evaluated as `true`. See the next section for usage.|

## How to monitor triggers (comparisons)
A trigger can be set to fire by comparing [Variables](_pages/Variables) with eachother. You can use this to e.g. play a sound when the player has collected half of the amount of crystals needed complete a objective.

	when(VALUE1>=VALUE2)[EVENT]

The above statement asks if VALUE1 is larger than or equal to VALUE2. If the expression evaluates to `true` then the trigger will activate the event. The **operator** in the middle can be replaced by anything from the table below.

!> Comparisons are not to be confused with conditions that are marked by double parenthesis `(())` although they work in a similar way.

?> The compared _values_ can be set to any valid float or integer variable, macro, class macro, function call, or regular numeric values. 

All variables used within a trigger are converted to integers which cuts off any decimals. This is different from rounding as if you compare 2.2 and 2.9 they will be equal. For more ideas on what you can use these for, please refer to [Macros](_pages/Macros).

|Logical operators|Meaning|
|---|---|
|>|Larger than|
|>=|Larger than or equal to|
|<|Less than|
|<=|Less than or equal to|
|==|Equal to|
|!=|Not equal to|
