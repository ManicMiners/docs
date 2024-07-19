# Arrays
Array variables are similar to arrays in most programming languages. Currently only integer arrays are supported.

Arrays allow multiple values to be stored and referenced by a single variable. They are highly useful in loops.

```mms
intarray SomeArray
```

The above creates an array variable. There is no way to initialize intarray to values, you must use script lines to initialize individual array indexes.

To put values in it you use `SomeArray[#]` where `#` is the position your values are to be saved in. Arrays begin with position 0 and end at the highest used position.

```mms
intarray SomeArray
	
MyChain::;
SomeArray[0]=123;
```	

If you put values in a position larger than the array size, the array automatically grows to fit.

```mms
intarray SomeArray

MyChain::;
SomeArray[0]=1;
SomeArray[1]=10;
SomeArray[2]=100;
SomeArray[3]=1000;
SomeArray[4]=10000;
```

In the above example `SomeArray` has 5 elements (indexes 0 - 4), each with its own value.

The index cannot be negative or the engine may crash.
If you skip indexes, the indexes that are not set are filled with 0.

```mms
intarray SomeArray

MyChain::;
SomeArray[0]=1;
SomeArray[2]=100;
SomeArray[4]=10000;
```

In the above, index 1 and index 3 are not set, thus they will have the value of 0 if read.
You cannot read an index beyond what the array has been set to.

```mms
intarray SomeArray
string MyMsg;

MyChain::;
SomeArray[5]=1;  # indexes 0-4 are set to 0.
MyMsg="Invalid reference ";
MyMsg+=SomeArray[6];   # not valid, index 6 has never been defined
```

The array index must be either a macro that returns an integer, a constant value, or an integer variable that has a valid index.

You cannot use nested arrays directly - the index cannot itself be an array. If you have need for this - for example using the value of one array as the index for another array - you must save the first array result into an integer variable and then use that integer variable.

There is no support for multi-dimensional arrays - only a single dimension is allowed. You may simulate a multi-dimensional array by using script to compute the resulting linear index.

There is currently no way to clear an array or to resize it.  If you are going to use arrays, generally you also need to maintain a count of the number of indexes used or the last used index.

