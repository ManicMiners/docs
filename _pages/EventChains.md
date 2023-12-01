# Event chains
You can declare multiple events as chains (functions). These may be called by if/when triggers, editor blocks that map to an event chain, or by each other.

Event chain names are defined by a valid name followed by two semi-colons and either a semi-colon or an event followed by a semi-colon.

```
	# You can write it like this...
	EVENT_CHAIN_NAME::EVENT;
	EVENT;
	EVENT; 

	#...or like this
	EVENT_CHAIN_NAME::;
	EVENT;
	EVENT;
```

- Event chain names follow the same rules as variables. They start with an alpha and are followed by optional alpha/digits. Using a reserved keyword as an event chain name will cause non-deterministic behaviors/errors just like variables.
- The `EVENT` events will execute in order as they are written.

!> After each event chain there should be an **empty line** to signal the end of the chain.

Event chains are similar to a subroutine call. Using the name will call the chain of events. When they have finished, control returns back to the caller.

## Init
The Init or Initialize event chain runs before any trigger can occurr in the level. This can be used to setup variables which need modification at runtime. The syntax is the same as any other event chain but the chain name must be Init.

```
	init::doStuff;
```

## tick
The tick event chain is called by the engine on EVERY engine tick. It is not recommended to be used unless that action taken by the script is very short. It would be far less overhead to use a timer that called script on some useful interval. Tick is called by the engine on every graphics frame update. 

```
	tick::doSomethingReallyShortAndFast;
```

## Conditions
Conditions can also be used together with event chains. They can be used with one or **optionally** two events.

```mms
	EVENT_CHAIN::EVENT;
	((CONDITION))[EVENT_TRUE][EVENT_FALSE];
	
	#if you only have the true case the syntax drops the []
	((CONDITION))EVENT;
```



The above statement fire `EVENT_TRUE` if ``((CONDITION))`` equals `true` or `EVENT_FALSE` if it equals `false`
## Example

```mms
	int counter=0	#A number
	string myStr="Counter: "	#A partial message
	string myMsg	#A blank string

	if(time:5)[myChain]	#A trigger
	
	myChain::;	#The Chain
	counter+=1;	#Increase the counter
	myMsg=myStr+counter;	#Combine a message
	msg:myMsg;	#Display the message
```
	
The above code run after 5 game-seconds, increases the counter from 0 to 1 and display a message to the player.

## Ending an Event Chain.

A blank line will end an event chain. In fact a trigger or variable statement will also end the event chain but that leaves you with very hard to read code. This means no blank lines (without comment) are allowed in an event chain. To make it easier for you to understand where the event chain ends, just have a blank line.

## return event

The return event will return from the current event chain. It is very useful to return from an event chain from the middle of logic.
```
    MyChain::;
    ((i<5))return;
    ((i>10))return;
    # continuing on will only be if i >=5 and <=10
```

## Looping

There is no traditional looping one would find in other languages. No for, while, until type of loops. There is no goto type of transfer control.
Every use of an event chain from a ((expression))[trueevent][falseevent] is a function call. An example best shows this:
```
    int i=0
    int sum=0;
    string s=""

    #loop 5 times
    myChain::i+=1;
    sum+=1;
    ((i<5))myChain;  #recursive call to myChain 5 times
    s="Sum: ";
    s+=sum;
    msg:s;
```
Run this example and you get 5 messages printed, all with the sum of 5.  The code after the conditional jump is executed for every iteration of the loop.  This can lead to unexpected results if the coder is not aware that each loop is a subroutine call.

Best practice is to end the event chain after the loop with a blank line. One may need to reorganize your logic to achive this.

The engine has a limit on the number of recursive calls active from any trigger - the total number of recursive event chains is somewhere around 890. Exceeding that may crash the game.

## Engine Tick Overhead

The Engine has what is known as a tick interval. This translates to the frame rate of the game if one has VSYNC disabled. There is a slider in the options to cap the frame rate to 350 FPS - which is the fastest tick interval.

if/when triggers are evaluated by the engine every tick. Note that there are many optimizations to avoid processing a trigger if some other conditions has not happen. For example a drill trigger will only be processed if a drill happen. Tile change will only be processed if a tile actually changed.

But some triggers require processing on every tick. An example:

```mms
when(air<100)[LowAirEvent]
```

The above will be computed on every tick. The same applies to use of any macro (air is a  macro) used in the condition of an if/when trigger. For best performance, try to minimize the use of these triggers.  The same applies to the tick:: event already described above.

##  Reentrancy

Timers and when triggers are subject to reentrancy - this is when the same code is executed at the same time.  For example lets say you have two drill triggers but they both call the same event. One can protect against this case by using the following code pattern:
```
int allowOnce=0

MyEvent::((allowOnce==0))[allowOnce=1][return];
# the following logic will only be executed once
```
This pattern can be extended into a semaphore type of control to only allow a single execution of the logic at any time - ignoring any attempts to run while the first one is running.
```
int oneAtATime=0

MyEvent::((oneAtATime==0))[oneAtATime=1][return];
# start of the logic
...
# end of the logic
oneAtATime=0;
```

Timer triggers can fire during the execution of the current event chain. Same for many movement / modification based triggers such as enter, drill, and change. Because the script only has global variables the script developer must be aware of these possible reentrancies.

## wait event and Reentrancy
The wait event will suspend the current event chain. During the time waiting, other timers and triggers are allowed to run. When the specific time duration has exprired, the event chain will then run the events after the wait event. Internally the engine deals with the same event being called by changing the name of the current running eventchain to an internal name that is slightly different and unique. Once the wait period has expired, it is renamed back to its original name.  There is nothing the script developer needs to do - this is an internal implementation. But it is how the same event can be executed while a prior event is executing the wait. Thus you can have multiple event chains waiting at the same time - including multiple invocations of the same event chain.
