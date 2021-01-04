# Arrays
Array variables act like a invisible list that can contain a lot of values with just one variable. Currently they can only *hold* integer values.

```mms
	intarray SomeArray
```

The above creates an array variable. To put values in it you use `SomeArray[#]` where `#` is the position your values are to be saved in. Arrays begin with position 0 and end at the highest used position.

```mms
	intarray SomeArray
	
	SomeArray[0]=123
```	

?> If you put values in a position larger than the array size, the array automatically resizes to fit.

!> Clearing or zeroing arrays are planned but not implemented yet.

## Example

```mms
	intarray mArray
	
	mArray[0]=get(2)(5)
```	
The above code gets the tile ID at row 2, column 5 and puts it into position 0 of the array.

