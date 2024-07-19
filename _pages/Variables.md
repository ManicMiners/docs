# Variables

Variables are containers for objects such as numbers and text. You can use them to keep track of values such as how many times the player has reinforced walls or how many caverns they have opened. Integer and float values are similar to what one would expect from any programming language.

Variables also are used with many classes:

- [arrow](_pages/ClassesArrow)
- [building](_pages/ClassesBuildings)
- [creature](_pages/ClassesCreatures)
- [miner](_pages/ClassesMiners)
- [timer](_pages/ClassesTimer)
- [vehicle](_pages/ClassesVehicles)

It is good practice to declare your variables at the start of the script before any other code - but it is not required. The script parse engine will first make a pass through the script looking for all variables (and event chain names) and initializing them. Then it makes a second pass processing all of the triggers and Event Chains. Thus you may reference variables and event chains prior to them being defined.

Variables have a type followed by a single space followed by a name. The name should not be one of the reserved events and macros - [list of reserved words](_pages/ReservedWords). Most variables have an optional initialization which is an equal sign after the name followed by the values(s).

## Variable Types

Variables can be of different types. Each type will only save certain values which means you have to use a type that can contain the value or text you want to save. Make sure to use a variable of the correct type to avoid errors.

|Variable|Declaration|Comment|
|----|----|----|
|arrow|arrow MyArrow=color|To be used with Arrow Events. Color may  be one of the following: `black`, `blue`, `darkgreen`, `green`, `red`, `yellow`, `white`. If no color is supplied, it defaults to green.|
|bool|bool HasFinishedTask=true|Saves true or false. Usable in conditions. Any initialization except "=true" is false. In Math events they are evaluated as 1 if true and 0 if false. By default it has a false value.|
|building|building MyHQ=3,4|This binds the building with a footpoint located at row 3, column 4 to the variable name. If unassigned, it may be later initialized with `lastbuilding` event.|
|creature|creature name=id|The creature identified by id is assigned to name. If unassinged it may be later assigned by `lastcreature`.|
|float|float MyFloatNumber=2.6|Saves decimal numbers. Like integer, you cannot auto initialized negative numbers. By default it has a value of 0.0|
|int|int MyInteger=5|Saves positive whole numbers. Any decimal number will be truncated - 2.9 will be shortened to just 2. You cannot auto initialized negative values. By default it has a valud of 0.|
|intarray|intarray MyArray|Defines an array of integers that will dynamically grow. No initialization values may be assigned and there are no default values for members of the array.|
|miner|miner Charlie=3|This binds the miner with the ID specified to the variable name at the time of initialization. If unassigned it may later be assigned a miner by `lastminer` event.|
|string|string MessStr="This is a message!"|Saves text. Numbers saved to strings are also considered text. There is no way to embed double quotes in the string itself.|
|timer|timer name=delay,min,max,eventchain|Defines a variable of type timer with the given name. It will wait delay seconds to start, and will fire between min seconds and max seconds after the last firing, calling the given eventchain. Timer values can be int or float. See Levels\DEMO\Scripts\demotimers.dat for example.|
|vehicle|vehicle BigBoye=2|This binds the vehicle with the ID specified to the variable name at the time of initialization. If unassigned, it may later be assigned a value with `lastvehicle` event.|


`creature`, `miner` and `vehicle` binds to the unit that currently holds the specified ID, not to the ID itself. These objects must exist in the map. They may located in undiscovered caverns. If the associated unit dies and another is assigned their ID, the associated events will NOT trigger.

`building` bind at the beginning of a level to the building at the given row,col and it may be in an undiscovered cavern. If the building is destroyed or teleports, then the variable is no longer bound to that building and any triggers using that building will not fire.

`creature`, `miner`, `vehicle` may be assigned to a specific unit with the = syntax. It is not allowed to have multiple variables point to the same object - this will lead to undefined behavior.
```mms
vehicle myTruck1=1    # vehicle id 1 is assigned to myTruck1
vehicle myTruck2=1    # ERROR, vehicle id 1 is already assigned to a variable
```
buildings are assigned by row,col, so even if the row,col is different, if it maps to the same building but at a different row,col it is still an error.
```mms
building myToolStore1=3,4   # building at 3,4 is assigned by myToolStore
building myToolStore2=3,5   # this may be an error if 3,5 is the same toolstore above
```

You can dynamically change `miner`, `vehicle`, `building` and `creature` variables with `lastminer`, `lastvehicle`, `lastbuilding` and `lastcreature` events but you cannot have triggers on those variables.

`arrow` variables are not real variables - they cannot be used in any context other than the events that specifically work with arrows. 

`timer` variables are not real variables - they cannot be used in any context other than the events that specifically work with timers.

`bool`, `int`, `float` work as expected compared to modern programming languages. Note that int and float cannot be initialized to a negative value but later may be given negative results.

## Mixing Variable Types

It is poor programming practice to mix bool and int variable types. For example, testing a bool variable to be > 0 - it works but not officially supported.  For bools the only logical operation types recommended are:
```mms
((var==true))
((var==false))
((var!=true))
((var!=false))
```
int and float types may freely be assigned or tested with each other. Floats are truncated toward 0 when assigned to an int. bools should not be assigned to int but it does work, false is 0 and true is 1.

Int and float values may be added to a string. For example:

```mms
string s=""
float fNow=0.0

init::;
fNow=time;   # get game time as a float
s="The current game time: "
s+=fNow;     # append floating point number to string
msg:s;       # display current game time
```
There is no way to convert strings to numeric values.

Variables of different types, ex, arrows, miners, buildings, etc, cannot be assigned to each other. The only variables that may be mixed are `bool`, `int`, and `float` but it is not good practice to mix `bool` with any other numeric type.

## Negative Constants

Negative constants are not supported by the parser. To assign a variable to a negative number or to use a negative constant, it must be computed at runtime usually from within an event chain.

```mms
int i

init::i=0-1;  # i is now -1
i=0-2;        # i is now -2
```

## Variable Names

Variable names (and Event Chains names) should follow standard programming variable names. The first character is an alpha followed by one or more alpha or digits. Names are case insensitive but case can be used to improve readability.  Variables do not have any special characters in them, just alpha followed by alphanumerics. There is no documented limit on the length of a variable name.

Technically the engine supports variables names (and Event Chains) that start with numeric(s) followed by at least one alpha and then optionally alphanumerics but it is really poor practice to do this - it violates modern programming standards. You will find this style in only a few older maps and is strongly discouraged.

>Note that the engine will not generate an error if a variable and event chain have the same name BUT you do get undefined behavior. Variables and Event Chains names must be unique.

As already stated above, variable names and event chain names must be unique and not one of the reserved words.  The script engine ignores case so variables cannot be unique by case alone. While case is ignored, it is a good practice to use case to improve readability.

