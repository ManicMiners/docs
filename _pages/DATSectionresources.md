# DAT Section resources

The resource section contains two parts - one is for crystals and the other is for ore.  These set the initial crystals and ore for every tile in the map.

Crystal and Ore values are positive integers. If the tile is a floor tile, then these crystals will be visible (assuming the floor tile itself is visible) on map load. If the tile is a wall, the wall must be drilled to reveal the crystals or ore. If the wall is not normally drillable, then some other mechanic must cause the wall to collapse (for example discovering a cavern).

Both the crystals and ore data are formatted in exactly the same way.

On a line by itself is the type of resource
- `crystals:`
- `ore:`

Starting on the next line is value for each tile in the map for that resource. This is identical to how the tiles section is formatted. There are rowcount rows of values, each line has colcount integers. Each integer value is followed by a comma with no space.

There may only be a single crystals and a single ore data. The order of them does not matter but the editor always writes the crystals section first.

Example for a 3x3 map that has 5 ore and 10 crystals in the middle tile of the map.

```mms
resources{
crystals:
0,0,0,
0,10,0,
0,0,0,
ore:
0,0,0,
0,5,0,
0,0,0,
}
```

Generally the map borders have 0 resources.

>While the upper limit on the number of resources per tile is not known, there are practical limits based on the physics engine. When resources are discovered by drilling/collapsing a wall, every resource is revealed by the physics engine as motion over time. Large values cause significant lag as the physics engine simulates each resource being revealed, trying to fall down the now collapsed wall. Attempting to put thousands of resources in a location will cause massive lag on even very fast machines - potentially making the map unplayable by the user.