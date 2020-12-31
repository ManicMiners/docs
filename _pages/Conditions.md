# Conditions
Inserting a condition before an event means the condition has to be true for the event to be executed.

`OCCURENCE(TRIGGER)((CONDITION))[EVENT_IF_TRUE]`
### Example
```
when(TRIGGER)((BOOLEAN==true))[EVENT]
when(TRIGGER)((crystals>30))[EVENT]
 ```
Where TRIGGER is any valid trigger, BOOLEAN is a variable of boolean-type and EVENT is any valid event.
###  Disclaimers
* A condition being false does NOT break or stop a event chain.
* IF-occurances with a condition are disabled and will therefore not fire even if you write them.

## Branches
A branch can select one of two events depending on a condition. If the condition equals `true` the first event is called, otherwise the second event is called.
### Example
```
 when(INTEGER>10)((air>=6000))[EVENT1][EVENT2]
```
Where INTEGER is any valid integer and EVENT is any valid event.
