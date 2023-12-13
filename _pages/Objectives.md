#  Objectives
You can bind objectives to scripting using the `variable` keyword.

<b>Note that this section is NOT in the script section but in the objectives section of the map file.</b>

The format is variable:EXPRESSION/OBJECTIVE

EXPRESSION is any valid variable expression and may use macros.
OBJECTIVE is a message seen by the player describing the objective.

```mms
variable:NumDrilledWalls>=10/Drill these 10 walls!
```

This will create an objective called `Drill these 10 walls!` that will be completed once the variable `NumDrilledWalls` contain a value of 10 or higher.

If all objectives are complete, the player will automatically win the map. If your logic wants to only win the map by using the win event you may need to put a final objective in the list that will only become true after your logic uses the win event.
