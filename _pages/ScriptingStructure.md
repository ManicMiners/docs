# Scripting structure
The scripting works by calling events from triggers. The structure looks like this:

```mms
OCCURRENCE(TRIGGER)((CONDITION))[EVENT1][EVENT2]
```
To make it work, replace each word with a proper scripting sentence.

## OCCURRENCE
This defines how many times a event can occur.

- `when` means the event can fire multiple times.
- `if` fires once, and then the trigger is removed forever.

## [TRIGGER](_pages/Triggers)
A trigger defines when the event should be called. It is marked with single parenthesis`()`. 

Triggers such as `walk` and `drive` fire once every time the tile is entered, not while someone is there.

## [CONDITION](_pages/Conditions)
A condition is an optional statement you can use to add a requirement to your script. This is marked with double parenthesis: `(())`. A condition allows you to compare two variables with each other and fire a event based on if the result equals `true` or `false`

## [Event](_pages/Events)
Events define what should happen. They are marked with square brackets: `[]` and can be written either one or two on the same line.

The first event is mandatory. It can be used with or without conditions. If it is used with conditions it will only fire if the condition equals `true`. The second event is **optional** and can only be used together with a condition. It will only fire if the condition equals `false`.

If you want to fire a bunch of events at once you can create a event chain. This is described in detail on the [Event chains](_pages/EventChains)-page.

## NO SPACES

Do not use spaces at the beginning of a line.
Do not use spaces at the end of a line.
Do not use spaces in the middle of a line. (see variables below)
Spaces are allowed inside of a string:  "  spaces are ok here"
Spaces are allowed after the end of a line if you have a comment.
A space is required between a variable declaration and its name.

## Example Scripts

It is highly recommended that one review the demo scripts provided with the game to understand the syntax rules. If you are wondering if it is known how to do something - these would be the best place to start your search. These are found in the location where Manic Miners is installed in the following subdirectory path: ManicMiners\Levels\DEMO\Scripts

## Reserved Words

A list of all known [reserved words](page/ReservedWords>). Do not use these for variable names or event chains.