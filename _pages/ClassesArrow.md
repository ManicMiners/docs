# Arrow class

Arrows are used for highlighting things in the world. Once you declare an arrow as a variable you can use these to move it around or hide it. The arrows have two usable components: A physical, hovering arrow, and a tile-sized highlight.

An arrow is initialized by using the arrow variable type.

```mms
arrow MyArrow=color
```

Color may be one of: `black`, `blue`, `darkgreen`, `green`, `red`, `yellow`, `white`

The arrow variable is then used by the following events.

|Event|Syntax|Description|
|---|---|---|
|hidearrow|hidearrow:ARROW|The arrow is hidden until manually shown again.|
|highlight|highlight:ROW,COLUMN,ARROW|Shows a highlight the size of a tile at ROW,COLUMN.|
|highlightarrow|highlightarrow:ROW,COLUMN,ARROW|Executes both showarrow and highlight at once.|
|showarrow|showarrow:ROW,COLUMN,ARROW|Shows the designated arrow at the tile ROW,COLUMN.|

It is highly recommended to review the Arrow examples in ManicMiners\Levels\DEMO\Scripts

Arrows were primarily put in for the tutorials and have limited use outside of tutorial type of maps - but it does allow the user to be notified of something they need to pay attention to by the map designer.

