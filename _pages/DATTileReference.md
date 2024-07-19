TileID's are used in the Dat tiles section and are also used in the script `place:` event.
There are two main types of tiles.
- floor tiles. These tiles allow traversal across (in some manner) and create the space for game play.
- wall tiles. These are two tiles thick and some are drillable. When a wall tile collapses, it becomes a floor tile, usually with rubble.

The info section contains rowcount and colcount - these are the height and width of the map. Note that the map border is usually solid rock regular (38).

Note that with script, the map designer is able to dynamically change a tile to any tile. When creating a new wall, it must be two tiles thick or it will collapse into a rubble tile.

|TileID|Type|Description|
|---|---|---|
|0|floor|invalid texture|
|1|floor|Ground|
|2|floor|Rubble Level 1|
|3|floor|Rubble Level 2|
|4|floor|Rubble Level 3|
|5|floor|Rubble Level 4|
|6|floor|Lava|
|7|floor|Erosion level 4|
|8|floor|Erosion level 3|
|9|floor|Erosion level 2|
|10|floor|Erosion level 1|
|11|floor|Water|
|12|floor|Slimy slug hole|
|13|floor|Power path in progress|
|14|floor|Power path building|
|15|floor|Power path building powered|
|16|floor|Power path 1|
|17|floor|Power path 1 powered|
|18|floor|Power path 2 adjacent|
|19|floor|Power path 2 adjacent powered|
|20|floor|Power path 2 opposite|
|21|floor|Power path 2 opposite powered|
|22|floor|Power path 3|
|23|floor|Power path 3 powered|
|24|floor|Power path 4|
|25|floor|Power path 4 powered|
|26|wall|Dirt regular|
|27|wall|Dirt corner|
|28|wall|Dirt edge|
|29|wall|Dirt intersect|
|30|wall|Loose rock regular|
|31|wall|Loose rock corner|
|32|wall|Loose rock edge|
|33|wall|Loose rock intersect|
|34|wall|Hard rock regular|
|35|wall|Hard rock corner|
|36|wall|Hard rock edge|
|37|wall|Hard rock intersect|
|38|wall|Solid rock regular|
|39|wall|Solid rock corner|
|40|wall|Solid rock edge|
|41|wall|Solid rock intersect|
|42|wall|Crystal Seam regular|
|43|wall|Crystal Seam corner|
|44|wall|Crystal Seam edge|
|45|wall|Crystal Seam intersect|
|46|wall|Ore seam regular|
|47|wall|Ore seam corner|
|48|wall|Ore seam edge|
|49|wall|Ore seam intersect|
|50|wall|Recharge seam regular|
|51|wall|Recharge seam corner|
|52|wall|Recharge seam edge|
|53|wall|Recharge seam intersect|
|54|wall|Biome specific|
|55|wall|Biome specific|
|56|wall|Biome specific|
|57|wall|Biome specific|
|58|wall|Roof|
|59|wall|Biome specific|
|60|floor|Fake rubble 1|
|61|floor|Fake rubble 2|
|62|floor|Fake rubble 3|
|63|floor|Fake rubble 4|
|64|wall|Cliff type 1 (experimental)|
|65|wall|Cliff type 2 (experimental)|

Floor tiles may have values that are +100. Those are undiscovered caverns and the map editor will automatically add the +100 value to those tiles during map save.  Wall tiles should not have the +100 values, since walls are never visible if the floor tile is also not visible.

During map read floor tiles that have the +100 value will be converted automatically to visible (the +100 will be removed) if the cavern is part of the open caves flag area.  When a cavern is discovered, all of the tiles discovered will have the +100 value removed from them.

Dirt, loose rock, hard rock may have a +50 value added to them. That means it has been reenforced so it cannot cause a landslide nor can monsters emerge from it.

>Tile 0 is special - it stands for invalid texture or empty. The engine may generate warnings when using tile 0. Do not intentionally place tile 0 via script.

The main wall types (dirt, loose rock, hard rock, solid rock, crystal Seam, Ore Seam, Recharge Seam) each have 4 different tiles. Unless you are trying to create a unique effect, there is only one that you use, the regular version. That tile will automatically be converted to the correct corner, edge, intersect by the game engine. The four types are:
- Regular, where it has 3 neighbor tiles and 2 diagonal neighbors adjacent to each other. In general these are the only wall tile id's used.
- Corner, where it has 4 neighbors and 3 diagonal neighbors
- Edge, where it has 2 neighbor tiles and 1 diagonal neighbors,
- Intersect, where it has 4 neighbors and 2 diagonal neighbors opposite to each other

The two cliff types are special - they act as walls but the wall is a single tile thick instead of the normal two tile think walls. They prevent movement across them and also prevent objects from moving across them. In general they are designed to deal with large differences in height to prevent vehicles, miners, and resources from falling down (and prevent monster from crossing them). Note that they are sometimes buggy but in general work.

Note that with script using the `place` event, you have access to tiles 1 - 175. Some have biome specific textures. Careful use some of id's can display interesting effects depending on biome. 

>Tiles 60 - 63 are floor tiles that have different amounts of rubble. None of that rubble will generate ore when cleared.