# Comments
Comments can be typed directly into the script. They are preceded by the `#` symbol. You can also use this to disable certain script lines.

The game engine ignores everything after the `#` comment character.  When added to a script line, the game engine will also ignore all spaces from the end of the script `;`

If an entire line is a comment, leading spaces prior to # are allowed

Having a comment line after the end of an event chain will not terminate the event chain - you still need a blank line.  Remember - a comment line is not the same as a blank line.

```mms
#This comments out the entire line, which is then ignored by the game.
        # this is also a valid full line comment, the leading spaces are ignored
 
init::disable:lights;      #This comment does NOT block the event on the same line.

MyChain::;
air+=100;    # give player 100 air
#  comment line does not end event chain but the blank line below does.

NewChain::;

```