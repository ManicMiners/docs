# Scripting structure

The scripting works by calling events from triggers. The structure looks like this:
```
OCCURENCE(TRIGGER)((CONDITION))[EVENT1][EVENT2] 
```
To make it work, replace each word with a proper scripting sentence.

## OCCURENCE

This defines how many times a event can happen, it can be either **when** or **if**.

**when** - Fires every time the trigger happens. Triggers such as _walk_ and _drive_ fire once every time the tile is entered, not while someone is there.

**if** - Fires once, and then the trigger is removed forever

## TRIGGER

A trigger defines when the event should be called. It is marked with single parenthesis: `()`. 

## CONDITION (optional)

Optionally you can add a condition to your script. This is marked with double parenthesis: `(())`. Inside conditions you can compare variables with each other and fire a event based on if the result equals `true` or `false`

## Event
Events define what should happen. They are marked with square brackets: `[]` and can be written either one or two on the same line.

The first event is mandatory. It can be used with or without conditions. If it is used with conditions it will only fire if the condition equals `true`. The second event is **optional** and can only be used together with a condition. It will only fire if the condition equals `false`.

If you want to fire a bunch of events at once you can create a event chain. This is described in detail on the [Event chains-page](example.com).
