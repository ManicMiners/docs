# Conditions

Conditions allow some sort of comparison and allow both true and false events to be called.  Only simple comparison conditions are allowed, complex and/or conditions or math operations are not supported.  Basically a left side can be compared to a right side.

`LHS`compare`RHS`

- `LHS` is the left hand side and can be a variable, macro, or numeric literal that returns a value. It is never modified.
- `compare` is one of the logical operations.
- `RHS` is the right hand side and can be a variable, macro or numeric literal that returns a value. It is never modified.

## Logical operators

|Logical operators|Meaning|
|---|---|
|>|Larger than|
|>=|Larger than or equal to|
|<|Less than|
|<=|Less than or equal to|
|==|Equal to|
|!=|Not equal to|


## Types of conditions
There are three types of conditions.
- Condition used as a trigger.
- Optional condition with a trigger.
- Condition event.


For a trigger, the conditions are describe as:

`OCCURENCE`(`TRIGGER`)((`OptionalCONDITION`))[`EVENT_IF_TRUE`][`OPTIONAL_EVENT_IF_FALSE`]

TRIGGER can be itself a comparison. For example:

```mms
if(air<500)[MyEvent]
```

This trigger will fire a single time once the air is under 500, calling the MyEvent event chain.  Notice that the trigger condition is surrounded with single braces. Notice that triggers do not end in a semi-colon.

A Trigger may have an optional CONDITION. It is surrounded with double braces just like an event condition.  What the engine does is wait for the given trigger to be true (in this case air<500) then it will evaluate the optional condition. If that is true the true event is executed, if it was false, the optional false event is executed

```mms
string msgbuildss="Hurry - build a support station!"
if(air<500)((BuildingSupportStation_C==0))[msg:msgbuildss]
```

In the above example, once the air falls below 500 the trigger will use the macro to return the number of Support Stations in the map, and if there are none - it will display a message telling the player to build a support station. The trigger that checks for air<500 will only happen a single time.

Event condition as part of an event chain is just like the optional condition for a trigger but it is now considered a single event. The format is:

```mms
((CONDITION))TRUEEVENT;                # only true case does anything
((CONDITION))[TRUEEVENT][FALSEEVENT];  # both true and false cases
```

Notice that for the event form, you end the statement with a semi-colon - all events as part of an event chain end with a semi-colon.


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

When using logical operators, the left side and the right side of the condition are never modified - they are read-only values.

Macros may be used in most expressions.

Collections may be used, they evaluate to an int that is the number of items in the collection.

## Do not mix types between the left side and the right side.

You cannot compare a string variable to a number. Or a building to a vehicle. Both left side and right side need to be the same. (TODO - can you even compare classes for == or != - never tried it. Also I have never tried to compare strings to strings) There are a few exceptions:

- floats may be compared to ints. The float is truncated for the comparison.
- bools may be compared to ints or floats, true is treated as 1 and false is treated as 0. Note it is poor programming to rely on this behavior, bools should only be compared to true or false. Thus with bools you should only use `==` or `!=`

## Emulating complex conditions

Conditions are only single comparisons - a left side variable or macro is compared to a right side variable or macro.  If your logic requires more than a single test you have to break up the logic into multiple tests - one at a time.

Here are some examples of patterns that can be used do compound tests:

Lets assume you need to check an x value and a y value to be in the range of 10,10 to 20,20. Psuedo code would be something like:

```mms
if (x >= 10) and (x <=20) and (y >= 10) and (y <= 20)) then
    true_event
else
    false_event
```

Pattern 1. Break up into multiple true chains.

```mms
MyChain::;
((x>=10))[checkxy1][falseevent];

checkxy1::((x<=20))[checkxy2][falseevent];

checkxy2::((y>=10))[checkxy3][falseevent];

checkxy3::((y<=20))[trueevent][falseevent];
```

With this pattern you keep spawning to a new event chain for the true condition. Its messy and does not scale well but does work correctly. You have early exits for false conditions.

Pattern 2. Simulate result using int var. Keep track of how many true conditions you have and check for that number of correct results.

```mms
int temp=0

MyChain::;
temp=0;
((x>=10))temp+=1;
((x<=20))temp+=1;
((y>=10))temp+=1;
((x<=20))temp+=1;
((temp==4))[trueevent][falseevent];   # all 4 tests are true or of them failed
```

This pattern scales well for complex tests. Only disadvantage is all tests have to be done - there is no early exit for the false condition.

Pattern 3 - invert tests and use return statement with a variable.

```mms
int temp=0

MyChain::;
MyTestXYChain;     # call a chain to do the tests
((temp==1))[trueevent][falseevent];

MyTestXYChain::;
temp=0;             # assume failure
((x<10))return;     # x too small
((x>20))return;     # x too large
((y<10))return;     # y too small
((y>20))return;     # y too large
temp=1;             # all tests pass, end of chain
```

This pattern scales well for large number of tests, you simply write a single event chain for all of the tests, and you test for the failure conditions and early return.

These patterns can be combined and/or nested to handle very complex if cases.

Dealing with logical OR cases can be done in a similar manner - you are just looking for any of the tests to pass.

