﻿
# Math
* [math](#math)
* [Extensions](#ext)
	* [round](#ext_round)


## math
The ``math`` library is a standard Lua library. It is a global library and does not need to be imported.

	math.abs(-123);			--> 123

Refer to the [official Lua documentation](http://www.lua.org/manual/5.1/) for more details.


## Extensions
Some additional math functions have been added.


### math.round( x )
Rounds the value ``x`` to the nearest integer (rounds 0.5 up).

	math.round(1.25);		--> 1
	math.round(1.5);		--> 2
	math.round(1.75);		--> 2
