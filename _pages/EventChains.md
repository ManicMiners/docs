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

Event chain names should all be unique and only defined a single time. Event Chain names should not be:
- A variable name.
- An already defined Event Chain name.
- [A reserved word.](_pages/ReservedWords)

>The script engine may not notify you in the logs of issues from duplicate names. If you have duplicate names it is considered undefined behavior.

Event chain names follow the same rules as variables. They start with an alpha or underbar and are followed by optional alphas/digits/underbars followed by two semi-colons. It is the two semi-colons that identify an Event Chain. Do not use any of the reserved words for the event chain name. Using a reserved keyword as an event chain name may cause undefined behaviors/errors just like variables. [list of reserved words](_pages/ReservedWords).

>Technically the engine supports Event Chain names (and variable names) that start with numeric(s) followed by at least one alpha or underbar - but it is really poor practice to do this - it violates modern programming standards. You will find this style in only a few older maps and is strongly discouraged. Thus it is `STRONGLY` encouraged that your variable names and event chain names start with either an alpha or underbar.

Within an event chain, the events will execute in order as they are written.

> After each event chain there should be an `empty line` to signal the end of the chain. See the note below about the technical rules that define the end of event chain.

Event chains are similar to a subroutine call. Using the name will call the chain of events. When they have finished, control returns back to the caller.

## Init
The `init::` event chain runs before any trigger is allowed to fire in the level. This may be used to setup variables which need modification at runtime. The syntax is the same as any other event chain but the chain name must be init.

```
	init::doStuff;
```

## tick
The tick event chain is called by the engine on EVERY engine frame update. It is not recommended to be used unless that action taken by the script is very short. It would be far less overhead to use a timer that called script on some useful interval. Tick is called by the engine on every graphics frame update - based on your vsync settings. Using tick may significantly impact framerate depending on what your event chain is performing.

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

All of these will end an event chain:
- blank line (highly recommended)
- comment line with leading space(s)
- Last event on the line does not have a semi-colon

>It is considered undefined behavior to not end an event chain via the above three methods.

Manic Miner scripting is already hard to debug. If you always have a blank line after an event chain, it helps in readability which always leads to fewer bugs.

- Having a comment with a leading space inside of an event chain always causes incorrect parsing by the engine but it may not show up in the logs at load time. These errors will show up in the runtime logs but may be hard to understand. Thus if you never have leading spaces for full line comments, you will never have this happen to you.
- Leaving the semi-colon off on the last event chain line also can lead to accidental errors if you leave off a semi-colon on an event inside of the event chain. This will end the event chain, and the remaining lines are now errors. If you just always end events inside of an event chain with semi-colons and use a blank line to end the event chain, you will avoid that error.

## No spaces after semi-colon ;
Spaces are not allowed after the semi-colon character `;`  unless there is a comment character after the sequence of spaces.  Having spaces after `;` is the single most common error one can make. To find spaces, use a good text editor with an option to show spaces like Visual Studio Code or Notepad++

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
    int sum=0
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

Contrary to previous versions of this document, new testing has determined that the script engine is always run in synchronous mode. This means that one never has to worry about multiple event chains running at the same time.

The engine has a queue of triggers waiting to be processed, and they are processed one at a time in the order they entered into the queue. 

Timers are a bit special, they have a min and max time. Once a timer is ready, it may jump to the head of the queue so it can be processed. It is not clear if this always happens, but testing does seem to indicate that timers have a slightly different priority than other triggers.  Like all triggers, the timer must return from its event chain before any other trigger or timer may run.

There is a wait event, this suspends the current event chain for a period of time, and allows other triggers to be executed.

If any timer or trigger event chain uses the following events, the current event chain is paused waiting for the action of that to finish:
- `drill:row,col`   Go drill that wall (and queue any other walls that collapse because of that) and execute its trigger.
- `place:row,col,tile`  Change the tile to another. This can cause the drill trigger if what you replace causes the wall to collapse or change to ground.
- `kill:unit`  Kill the miner, building, creature causing its .dead trigger to fire. That trigger will run and then return.
- `wait:time`  Pause the current event chain for the given time period. It allows any other trigger to execute.

What this means is that using place, drill, kill, or wait can cause another trigger to be called and your event chain will wait for that to return before continuing.

Example:
```
when(enter:5,4)[entered54]
if(drill:5,6)[didDrill56]
if(drill:6,7)[didDrill67]

entered54::;  # when unit enter this tile
drill:5,6;    # drill 5,6. Wait until that drill trigger finishes
drill:6,7;    # drill 6,7. Wait until that drill trigger finishes

didDrill56::;
# do whatever

didDrill67::;
# do whatever
```
When a unit enters the 5,4 tile, it will start the entered54 event chain. That chain will drill the 5,6 wall and wait for the drill trigger to finish. Then it will drill the 6,7 wall and wait for that drill trigger to finish.

> Using drill, place, kill, or wait can cause other triggers to run. You must be careful in your event chain calling sequences to guard against the same code being called again.  Remember - script only has global variables so event chains do not have local variables. Thus the script developer needs to make sure their global variables are not unintentionally changed.

## wait event

The wait event is special. What it does is tell the current event chain to pause for a bit, with the wait value specified by the parameter.

While not generally useful, you can use `wait:0` to pause your event chain for as short as possible but give other pending triggers a chance to run.

Pausing an event chain has a special side effect - it allows other triggers to execute.  So if there triggers waiting to run, they will get a chance to run.  Thus it is possible that through other triggers, your same code can be called again - this is call reentrancy.

## protecting timers from reentrancy

In particular, timers should check for this.  The following code snippet is one way to protect timers.

```
bool bInMyTimer=false

MyTimer::;
((bInMyTimer==false))[bInMyTimer=true][return];  # ignore if already inside
# do your logic
# end of your logic
bInMyTimer=false;   # no longer inside
```

Generally timers are safe to do this to since a timer just a way to do some sort of regular processing and ignoring a timer should not change your behavior.


## Special Event Modifiers
See [Events](_pages/Events) for description of the event `?` and `~` modifiers - they only are used within an Event Chain.