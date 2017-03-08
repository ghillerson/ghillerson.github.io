[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Ceil.html)

<a href="" id="BuiltInFcns.Ceil"></a>[]()CEIL or []()CEILING
============================================================

The <span class="CodeFont">CEIL</span> and <span class="CodeFont">CEILING</span> functions round the specified number up, and return the smallest number that is greater than or equal to the specified number.

Syntax

``` FcnSyntax
CEIL ( number )
```

``` FcnSyntax
CEILING ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) value.

The expression can contain multiple column references or expressions, but it cannot contain another aggregate or subquery, and it must evaluate to an ANSI SQL numeric data type. This means that you can call methods that evaluate to ANSI SQL data types.

If an expression evaluates to <span class="CodeFont">NULL</span>, the aggregate skips that value.

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

The returned value is the smallest (closest to negative infinity) double floating point value that is greater than or equal to the specified number. The returned value is equal to a mathematical integer.

-   If the specified number is <span class="CodeFont">NULL</span>, the result of these functions is <span class="CodeFont">NULL</span>.
-   If the specified number is equal to a mathematical integer, the result of these functions is the same as the specified number.
-   If the specified number is zero (0), the result of these functions is zero.
-   If the specified number is less than zero but greater than -1.0, then the result of these functions is zero.

Example

``` Example
splice> VALUES CEIL(3.33);
1
----------
4

1 row selected

splice> VALUES CEILING(3.67);
1
----------
4

1 row selected
```

See Also

-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


