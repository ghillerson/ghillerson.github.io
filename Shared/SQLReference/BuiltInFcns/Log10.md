[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Log10.html)

<a href="" id="BuiltInFcns.Log10"></a>[]()LOG10
===============================================

The <span class="CodeFont">LOG10</span> function returns the base-10 logarithm of the specified number.

Syntax

``` FcnSyntax
LOG10 ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number that is greater than zero (<span class="CodeFont">0</span>).

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

-   If the specified number is <span class="CodeFont">NULL</span>, the result of this function is <span class="CodeFont">NULL</span>.
-   If the specified number is zero or a negative number, an exception is returned that indicates that the value is out of range (SQL state 22003).

Example

``` Example
splice> VALUES LOG10(84.4);
1
----------
1.926342446625655

1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


