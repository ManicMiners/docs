# Comments
Comments are notes to the developer that do not have any action to the script engine - they are ignored when reading in the map. They are preceded by the `#` symbol. You can also use this to disable certain script lines.

The game engine ignores everything after the `#` comment character.  When added to a script line, the game engine will also ignore all spaces from the end of the script `;`

If an entire line is a comment, leading spaces prior to # are allowed, with restrictions.
Within the middle of an event chain, you CANNOT have comments that start with leading spaces. This will terminate the current event chain and the following lines will generate an error since they are no longer inside of an event chain.

Having a comment line after the end of an event chain will not terminate the event chain unless it has one or more leading spaces.

Given that there are rules associated with comment line and leading spaces, it is recommended to not have any leading spaces for comment lines - that way there is consistent behavior.

```mms
#This comments out the entire line, which is then ignored by the game.
        # not recommended, valid full line comment, the leading spaces are ignored
 
init::disable:lights;      #This comment does NOT block the event on the same line.

MyChain::;
air+=100;    # give player 100 air
#comment line does not end event chain but the blank line below does.
crystals+=1; # give player a crystal

NewChain::;

```