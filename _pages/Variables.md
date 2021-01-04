# Variables

Variables are containers for values or text. You can use them to keep track of values such as how many times the player has reinforced walls or how many caverns they have opened.

Always declare your variables at the start of the script before any other code. You do this by giving them a type and a name (see below). You can name a variable to almost anything and when you later use that name in a script it will be replaced by the value or text you saved to it.

## Variable Types

Variables can be of different types. Each type can only save certain values which means you have to use a type that can contain the value or text you want to save. Make sure to use a variable of the correct type to avoid errors.

|Variable|Declaration|Comment|
|----|----|----|
|string|string MessStr="This is a message!"|Saves text. Numbers saved to strings are also considered text. Citations are not a requirement yet.
|integer|int MyInteger=5|Saves whole numbers. Any decimal number will be trunctuated I.eg. 2.9 will be shortened to just 2.|
|float|float MyFloatNumber=2.6|Saves decimal numbers.|
|boolean|HasFinishedTask=true|Saves true or false. Usable in conditions. Any initialization except "=true" is false. In Math events they are evaluated as 1 if true and 0 if false.|
|miner|miner Charlie=3|This binds the miner with the ID specified to the variable name at the time of initialization.*|
|vehicle|vehicle BigBoye=2|This binds the vehicle with the ID specified to the variable name at the time of initialization.*|
|building|building MyHQ=3,4|This binds the building with a footpoint on tile on row 3, column 4 to the variable name at the time of initialization.**|
|arrow|arrow MyArrow / arrow MyArrow=color|To be used with [Arrow Events](_pages/Events). Color represent the color to highlight the tile beneth the arrow and can be one of the following: ''red, green, blue, darkgreen, yellow, white, black''|


?> **\*** **miner** and **vehicle** binds to the unit that currently holds the specified ID, not to the ID itself. If the associated unit dies and another is assigned their ID, the associated events will NOT trigger.<br>**\*\*** **Buildings**, **miners** and **vehicles** bind at the beginning of a level which mean that if a bound unit or structure is teleported or destroyed then any associated events will no longer trigger.
