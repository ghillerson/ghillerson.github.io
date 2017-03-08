[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Floor.html)

<a href="" id="BuiltInFcns.Floor"></a>[]()FLOOR
===============================================

The <span class="CodeFont">FLOOR</span> function rounds the specified number down, and returns the largest number that is less than or equal to the specified number.

Syntax

``` FcnSyntax
FLOOR ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

Example

``` Example
splice> VALUES FLOOR(84.4);
1
----------
84

1 row selected
```

Results

The data type of the result is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number. The returned value is equal to a mathematical integer.

-   If the specified number is <span class="CodeFont">NULL</span>, the result of this function is <span class="CodeFont">NULL</span>.
-   If the specified number is equal to a mathematical integer, the result of this function is the same as the specified number.
-   If the specified number is zero (<span class="CodeFont">0</span>), the result of this function is zero.

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


