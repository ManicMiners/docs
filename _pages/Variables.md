# Variables

Variables are containers for values or text. You can use them to keep track of values such as how many times the player has reinforced walls or how many caverns they have opened. <span style='background-color:#ff2e63;'>They can also read values from the level such as the current crystal count or the amount of miners in the level.</span>

Always declare your variables at the start of the script before any other code. You do this by giving them a type and a name (see below). You can name a variable to almost anything and when you later use that name in a script it will be replaced by the value or text you saved to it.

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
|arrow|arrow MyArrow / arrow MyArrow=color|To be used with [[Scripting#Arrow events|LINK]]. Color represent the color to highlight the tile beneth the arrow and can be one of the following: ''red, green, blue, darkgreen, yellow, white, black''|


*_miner_ and _vehicle_ binds to the unit that currently holds the specified ID, not to the ID itself. If the associated unit dies and another is assigned their ID, the associated events will NOT trigger.

**_Buildings_, _miners_ and _vehicles_ bind at the beginning of a level which mean that if a bound unit or structure is teleported or destroyed then any associated events will no longer trigger.

## Macros
There are variable names that are reserved as macros which cannot be overwritten. When used in scripting, these can return and in some cases set a value. You can use macros to e.g. show a message when the player has collected 3 crystals or to trigger a monster invasion if the player constructs too many buildings (with a fair warning first).

### Macros without input

|Macro|Return Type|Function|
|----|----|----|
|crystals|Integer or null|Returns the crystal count*|
|ore|Integer or null|Returns the ore count*|
|studs|Integer or null|Returns the studs count*|
|air|Integer|Returns the air status in miner-seconds*|
|miners|Integer|Returns the amount of miners|
|vehicles|Integer|Returns the amount of vehicles|
|buildings|Integer|Returns the amount of buildings|
|time|Integer|Returns the amount of seconds that have passed since the level began.|
|[[Classes|LINK]]|Integer|Returns the amount of existing units/buildings of the specified class.**|
|lastminer||Return the last miner that activated a trigger.|
|lastvehicle||Return the last vehicle that activated a trigger.|
|lastbuilding||Return the last building that activated a trigger.|
|ConstructedBuilding||Return the last constructed building.|
|datafield|various|properties that return information about a unit or building. See [[Datafields]] for more info.|
*These macros can also be used to directly set the current gathered resources (such as crystals=5).

**You can fetch the current count of any class in the game if you know the name of it. A full list of classes is [https://manicminers.fandom.com/wiki/Classes available here]. Buildings and vehicles **will only monitor non-hidden units**.

### Macros with input
These macros requires input values in order to function.

|Macro|Return Type|Description|
|----|----|----|
|random(MIN)(MAX)|Integer or float|Return a random number in the range [MIN-MAX]. Can be used with both integers and floats.|