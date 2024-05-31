#  Objectives
<b>Note that this section is NOT in the script section but in the objectives section of the map file.</b>

In the message box area of the UI during map play there is an objectives tab - the text messages displayed there come from this section of the map. Once an objective is complete, it is marked with a green check-mark.

This means that objectives are not changeable at run time - they are loaded at map load time. Thus they are always shown.  Using this section you cannot have hidden objects that then become active.

You bind objectives to scripting using the `variable` keyword.

The format is variable:`EXPRESSION`/`OBJECTIVE`

Each objective is a single line and starts with the `variable:` keyword. After that is the name of a single variable that is defined in the script section or one of the predefined macros. It is then followed by one of the comparison operators, followed by what it is compared to.

EXPRESSION is any valid variable expression and may use macros. It is subject to the same limitations as script expressions so it cannot be compound and cannot include math operators.

A forward slash ends the EXPRESSION portion, following it is the OBJECTIVE text.

OBJECTIVE is a message seen by the player describing the objective and cannot be changed during map play.


```mms
variable:NumDrilledWalls>=10/Drill these 10 walls!
```

This will create an objective called `Drill these 10 walls!` that will be completed once the variable `NumDrilledWalls` contain a value of 10 or higher.

Once any objective has been marked as complete, the game engine no longer checks for it. For example if you want the user to make 5 toolstores, once they have 5 toolstores that objective is done - it is checked as complete in the UI and the game no longer checks for that. Thus the player could delete the toolstores but the objective is still complete.

If all objectives are complete, the player will automatically win the map. If your logic wants to only win the map by using the win event you may need to put a final objective in the list that will only become true after your logic uses the win event.

Here is a more complex example. You have a map called Area51 and the goal is to build 4 Support Stations, fill the caven with a lot of air, and discover two areas of the map. In addition there is a final objective when you learn the true secret of Area 51.

```mms
variable:BuildingSupportStation_C>=4/Build 4 Support Stations.
variable:air>3000/Fill the cavern with air.
variable:AreaAfound==true/Discover area Alpha.
variable:AreaBfound==true/Discover area Beta.
variable:Area51Secret==true/Uncover the Secret of Area 51!
```

In the above case two of the objectives are using predefined macros. Three of the cases are using bools that you will declare in the script section of the map. Your logic in the script section will set each bool to true when the conditions you have coded up have been met.  When all five conditions are marked as complete, the user wins the map.

While the text in the objectives section cannot be changed, from within your script logic there is nothing preventing you from having additional objectives for the user to complete. They cannot be shown in the objectives tab, but you may display any message to the user by using `msg:` or `qmsg:`  If you do this, consider that the user may not see your message so you may need to occasionally remind them...

