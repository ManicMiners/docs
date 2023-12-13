# Variables

Variables are containers for objects such as numbers and text. You can use them to keep track of values such as how many times the player has reinforced walls or how many caverns they have opened. Integer and float values are similar to what one would expect from any programming language.

It is good practice to declare your variables at the start of the script before any other code - but it is not required. The script parse engine will first make a pass through the script looking for all variables (and event chain names) and initializing them. Then it makes a second pass processing all of the triggers and Event Chains. Thus you can use variables and event chains prior to them being defined.

Variables have a type followed by a single space followed by a name. The name should not be one of the reserved events and macros - [list of reserved words](_pages/ReservedWords). Variables have an optional initialization which is an equal sign after the name followed by the values(s).

## Variable Types

Variables can be of different types. Each type will only save certain values which means you have to use a type that can contain the value or text you want to save. Make sure to use a variable of the correct type to avoid errors.

|Variable|Declaration|Comment|
|----|----|----|
|arrow|arrow MyArrow=color|To be used with [Arrow Events](_pages/Events). Color represents the color to highlight the tile beneth the arrow and can be one of the following: `black`, `blue`, `darkgreen`, `green`, `red`, `yellow`, `white`|
|bool|bool HasFinishedTask=true|Saves true or false. Usable in conditions. Any initialization except "=true" is false. In Math events they are evaluated as 1 if true and 0 if false.|
|building|building MyHQ=3,4|This binds the building with a footpoint located at row 3, column 4 to the variable name.|
|creature|creature name=id|The creature identified by id is assigned to name|ex: creature PetMonster=5   Id's are from the creature section, the ID= field.|
|float|float MyFloatNumber=2.6|Saves decimal numbers. Like integer, you cannot auto initialized negative numbers.|
|int|int MyInteger=5|Saves positive whole numbers. Any decimal number will be truncated - 2.9 will be shortened to just 2. You cannot auto initialized negative values.|
|intarray|intarray MyArray|Defines an array of integers that will dynamically grow.|
|miner|miner Charlie=3|This binds the miner with the ID specified to the variable name at the time of initialization.*|
|string|string MessStr="This is a message!"|Saves text. Numbers saved to strings are also considered text.
|timer|timer name=delay,min,max,eventchain|Defines a variable of type timer with the given name. It will wait delay seconds to start, and will fire between min seconds and max seconds after the last firing, calling the given eventchain. Timer values can be int or float. See Levels\DEMO\Scripts\demotimers.dat for example.|
|vehicle|vehicle BigBoye=2|This binds the vehicle with the ID specified to the variable name at the time of initialization.*|


?> **creature**, **miner** and **vehicle** binds to the unit that currently holds the specified ID, not to the ID itself. These objects must exist in the map. If the associated unit dies and another is assigned their ID, the associated events will NOT trigger.

**building**, **creature**, **miner** and **vehicle** bind at the beginning of a level which mean that if a bound unit or structure is teleported or destroyed then any associated events will no longer trigger.

You can dynamically change `miner`, `vehicle`, `building` and `creature` variables with `lastminer`, `lastvehicle`, `lastbuilding` and `lastcreature` events but you cannot have triggers on those variables.

## Mixing Variable Types

It is good programming practice to not mix bool and int variable types. For example, testing a bool variable to be > 0 - it works but not officially supported.  For bools the only logical operation types recommended are:
```mms
((var==true))
((var==false))
((var!=true))
((var!=false))
```
int and float types may freely be assigned to each other. Floats are truncated toward 0 when assigned to an int. bools should not be assigned to int but it does work, false is 0 and true is 1.

Int and float values may be added to a string. For example:

```mms
string s="The current game time: "
float fNow=0.0

init::;
fNow=time;   # get game time as a float
s+=fNow;     # append floating point number to string
msg:s;       # display current game time
```
There is no way to convert strings to numeric values.
Variables of different types, ex, arrows, miners, buildings, etc, cannot be assigned to each other.

## Negative Constants

Negative constants are not supported by the parser. To assign a variable to a negative number or to use a negative constant, it must be computed at runtime usually from within an event chain.

```mms
int i

init::i=0-1;  # i is now -1
i=0-2;        # i is now -2
```

## Variable Names

Variable names (and Event Chains names) should follow standard programming variable names. The first character is an alpha followed by one or more alpha or digits. Names are case insensitive but case can be used to improve readability.

Technically the engine supports variables names (and Event Chains) that start with a numeric followed by at least one alpha but it is really poor practice to do this - it violates modern programming standards. You will find this style in only a few older maps and is strongly discouraged.

## Timers

Periodic timers are created by either the visual block system or use of a timer variable. Once a timer is created, it will continue to fire on the given interval until the user exits the map. The interval values may be floating point numbers and the engine does support sub second timings. Naturally as timers fire faster or the more timers are active - internal overhead associated with them increases. That said, using timers is always more efficient than using the `tick` Event Chain.

Using a timer variable allows use of `stoptimer` and `starttimer` events.