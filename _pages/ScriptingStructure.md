# Scripting structure
Scripting is text inside the Script section of the .DAT file. There are five types of lines that are found inside this section.
- comments. [Comments](_pages/Comments) start with a `#` character and continue until the end of the line.
- variables. [Variables](_pages/Variables) provide storage for values or objects to modify.
- triggers. [Triggers](_pages/Triggers) are notifications from the engine to the script allowing logic changes. Every action a script is able to do starts with a trigger. Triggers may use a single event or call Event Chains.
- Events. [Events](_pages/Events) are a single operation and they are what a trigger will use.
- [Event Chains](_pages/EventChains) are multiple events assigned to a name, they are similar to a function call in other languages. Since the name is itself now considered a single event, it may be called by triggers, the block system or by other Event Chains.

The general logic flow of a script is to have trigger(s) to respond to gameplay. When those triggers are invoked (trigger fires), the script runs performing some action by using event(s). If the action is simple the trigger may only use a single event. If the action is more complex, the trigger is able to call an Event Chain to perform a sequence of actions. The script then returns from the trigger.  This process continues until the map is exited.

If the map is either won or lost, most triggers will continue to fire until the user exits the map. This allows gameplay to continue after the map is won.

There are two predefined hidden triggers and they call special Event Chains in the script. If you have an Event Chain called `init` that Event Chain will be called once at the start of the gameplay prior to any other trigger in the map firing. This is very useful to perform one time initializations. If you have an Event Chain called `tick` that Event Chain will be called on every game engine frame update. See [Event Chain](_pages/EventChains) for more information on these.

There are two types of triggers.
- Single call triggers defined using `if`. They are only called a single time.
- Multiple call triggers defined using `when`. They are called every time the trigger condition is true. 

The format of a trigger is:

```mms
OCCURRENCE(TRIGGER)((CONDITION))[TRUE_EVENT][FALSE_EVENT]
```
## OCCURRENCE
This defines how many times a event can occur.

- `if` fires once, and then the trigger is removed forever.
- `when` means the event can fire multiple times.

## [TRIGGER](_pages/Triggers)
A trigger defines when the event should be called. The trigger itself is inside of the single parenthesis`()`. 

Triggers such as `walk` and `drive` fire when the tile is entered, not while someone is there.

## [CONDITION](_pages/Conditions)
A condition is an optional statement you can use to add a requirement to your script. This is identical to a condition inside of an event chain. The conditional test is inside of double parenthesis: `(())`. A condition allows you to compare two variables with each other and fire a event based on if the result equals `true` or `false`

>Note that an `if` trigger is only executed a single time. If the trigger check is true - the trigger fires and then checks the conditional. The value of the conditional (true/false) only decides which event is called - either the true event or the false event. In either case, the trigger will never fire again.

## [Event](_pages/Events)
Events define what should happen. They are contained inside square brackets: `[]`. There is always a true event and an optional false event.

Events may be a single statement or an Event Chain name to execute multiple statements.

The first event is mandatory. It can be used with or without conditions. If it is used with conditions it will only fire if the condition is true. The second event is optional and can only be used together with a condition. It will only fire if the condition is false.

Examples:
```mms
# display message after every Ice Monster leaves map.
when(CreatureIceMonster_C.dead)[msg:DeadIceMonMsg]

# call Event Chain when the first unit enters row 1 col 2 tile and then never call again.
if(enter:1,2)[MyEnterChain]

# call either EnoughCrystals or TooFewCrystals every time a unit enters row 3 col 4 tile.
when(enter:3,4)((crystals>10))[EnoughCrystals][TooFewCrystals]  
```

## No Spaces

- Do not use spaces at the beginning of a line.
- Do not use spaces at the end of a line.
- Do not use spaces in the middle of a line. (see variables below)
- Spaces are allowed inside of a string:  "  spaces are ok here"
- Spaces are allowed after the end of a line if you have a comment.
- A space is required between a variable declaration and its name.

## Example Scripts

It is highly recommended that one review the demo scripts provided with the game to understand the syntax rules. If you are wondering if it is known how to do something - these would be the best place to start your search. These are found in the location where Manic Miners is installed in the following subdirectory path: ManicMiners\Levels\DEMO\Scripts

## Reserved Words

A list of all known [reserved words](_pages/ReservedWords). Do not use these for variable names or event chains.

## Order of coordinates

All events that use row, col are always row first followed by col. Row maps to Y and col maps to X. This will confuse those that would expect the normal order of X,Y used in most vector and graphics systems. The level editor always shows coordinates as row,col.

Remember - everything that uses coordinates ALWAYS use row,col.