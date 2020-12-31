# Triggers
A trigger activates in response to things that happen in the world, such as a wall being drilled or a miner walking over a tile. 

|Trigger|Syntax|Description|
|----|----|----|
|drill|(drill:ROW,COLUMN)|Call the corresponding event when a wall at ROW,COLUMN is drilled, or the wall there collapses.|
|built|(built:ROW,COLUMN)|Call the corresponding event when a building is built upon the specified coordinate.|
|laser|(laser:ROW,COLUMN)|Call the corresponding event when a wall at ROW,COLUMN is destroyed by a laser.|
|laserhit|(laserhit:ROW,COLUMN)|Call the corresponding event when a wall at ROW,COLUMN is hit by a laser, but not destroyed.|
|change|(change:ROW,COLUMN / (change:ROW,COLUMN,ID)|Call the corresponding event when a wall at ROW,COLUMN is changed in any way. This includes reinforcing, shoveling once, drilling, finding a cave etc. Optionally add a ID requirement for the trigger to fire only if the tile is changed to a specific tile ID.|
|reinforce|(reinforce:ROW,COLUMN)|Call the corresponding event when a wall at ROW,COLUMN is reinforced by any unit.|
|time|(time:SECONDS)|Call the corresponding event when SECONDS seconds have been reached. Supports decimal floats.|
|hover|(hover:ROW,COLUMN)|Activates when the player hovers that tile. The tile has to be visible.|
|click|(click:ROW,COLUMN)|Activates when the player clicks that tile. The tile has to be visible.|
|walk|(walk:ROW,COLUMN) / (walk:ROW,COLUMN, NAME)|Activates when a [[Classes|LINK]] walks on a tile. Optionally add a NAME requirement to make the trigger fire only for a specific class.*|
|drive|(drive:ROW,COLUMN) / (drive:ROW,COLUMN, NAME)|Activates when a [[Classes|LINK]] is driven over a tile. Optionally add a NAME requirement to make the trigger fire only for a specific class.*|
|enter|(enter:ROW,COLUMN) / (enter:ROW,COLUMN, NAME)|Activates when a [[Classes|class]] enters a tile, either miner or vehicle. Optionally add a NAME requirement to make the trigger fire only for a specific class.*|
|comparison|(''expression'')|Activates when the ''expression'' is evaluated as `true`. See the next section for usage.|
*ID only works with named miner or vehicle variables. 

## How to monitor triggers
A trigger can be set to fire by comparing Variables and macros. You can use this to e.g. play a sound when the player has collected half of the amount of crystals they need to complete the level.

`(VALUE1>=VALUE2)`

The above statement asks if VALUE1 is larger than or equal to VALUE2. If the expression evaluates to `true` then the trigger will activate a following event. This is not to be confused with conditions that are marked by double parenthesis `(())` although they work almost exactly the same. The _operator_ in the middle can be replaced by anything from the table below.

The _values_ can be set to any valid float or integer variable, macro, class macro, function call, or regular numeric values.  All variables used within a trigger are converted to integers which cuts off any decimals. This is different from rounding as if you compare 2.2 and 2.9 they will be equal. For more ideas on what you can use these for, please refer to the [[Scripting#Macros|LINK]].

|Comparison operators||
|---|---|
|>|Larger than|
|>=|Larger than or equal to|
|<|Less than|
|<=|Less than or equal to|
|==|Equal to|
|!=|Not equal to|