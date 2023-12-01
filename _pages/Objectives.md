#  Objectives
You can bind objectives to scripting using the `variable` keyword.

<b>Note that this section is NOT in the script section but in the objectives section of the map file.</b>

```
variable:NumDrilledWalls>=10/Drill these 10 walls!
```

This will create an objective called `Drill these 10 walls!` that will be completed once the variable `NumDrilledWalls` contain a value of 10 or higher.