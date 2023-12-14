# Conditions
There are two types of conditions.
- Conditions as part of a trigger.
- Conditions as part of an Event Chain.

Conditions allow some sort of comparison and allow both true and false events to be called.

For a trigger, the conditions are describe as:

`OCCURENCE(TRIGGER)((CONDITION))[EVENT_IF_TRUE][OPTIONAL_EVENT_IF_FALSE]`
### Example

```mms
when(TRIGGER)((MyBoolVar==true))[EVENT_TRUE][OPTIONAL_EVENT_FALSE]
```

As part of an Event Chain there is no if/when/trigger parts so it is used like this:
- `((CONDITION))EVENT_TRUE;`
- `((CONDITION))[EVENT_TRUE][EVENT_FALSE];`

```mms
((MyBoolVar==true))EVENT_TRUE;
((i!=j))[EVENT_TRUE][EVENT_FALSE];
```

Notice that when used in Event Chains, if there is no optional false event, the square brackets are not used for the true event.

The logic flow for a condition in Event Chains is:
- if true, call the true event;
- if false, call the false event if there is one.
- execution of the script continues after the called events return.

Remember, every Event Chain used is itself a subroutine call so the calling Event Chain will wait until the called Event Chain finishes.  See the [Event Chain](_pages/EventChains) for more info about recursion.

## Logical operators

|Logical operators|Meaning|
|---|---|
|>|Larger than|
|>=|Larger than or equal to|
|<|Less than|
|<=|Less than or equal to|
|==|Equal to|
|!=|Not equal to|

When using logical operators, the left side and the right side of the expression are never modified - they are read-only values.

Macros may be used in most expressions.

Collections may be used, they evalulate to an int that is the number of items in the collection.