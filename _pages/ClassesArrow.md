# Arrow class

Arrows are used for highlighting things in the world. Once you declare an arrow as a variable you can use these to move it around or hide it. The arrows have two usable components: A physical, hovering arrow, and a tile-sized highlight.

An arrow is initialized by using the arrow variable type.

```mms
arrow MyArrow=color
```

Color may be one of: `black`, `blue`, `darkgreen`, `green`, `red`, `yellow`, `white`

The default color for an arrow variable is green, so these two statements are the same:
```mms
arrow MyArrow1
arrow MyArrow2=green
```

Note that the color of the arrow is not the arrow color - all arrows look and are colored the same. The highlight patch is what the color is used for.


The arrow variable is then used by the following events.

|Event|Syntax|Description|
|---|---|---|
|hidearrow|hidearrow:ARROW|The arrow is hidden until manually shown again.|
|highlight|highlight:ROW,COLUMN,ARROW|Starts a blinking highlight of the tile at ROW,COLUMN in the color of the arrow|
|highlightarrow|highlightarrow:ROW,COLUMN,ARROW|Executes both showarrow and highlight at once.|
|showarrow|showarrow:ROW,COLUMN,ARROW|Shows the designated arrow at the tile ROW,COLUMN.|

It is highly recommended to review the Arrow examples in ManicMiners\Levels\DEMO\Scripts

Arrows have two display properties. First is the bouncing arrow - all arrow variables draw the exact same arrow. Arrows also have a highlight property - this is the blinking highlight of the tile in the color of the arrow variable.   `showarrow` only shows the arrow, `highlight` only shows the highlight, `highlightarrow` does both at the same time.

Arrows were primarily put in for the tutorials and have limited use outside of tutorial type of maps - but it does allow the user to be notified of something they need to pay attention to by the map designer.

Arrow variables `cannot be assigned to each other`. They cannot be used in any expression, conditional or assignment and may only be used with the above events.
