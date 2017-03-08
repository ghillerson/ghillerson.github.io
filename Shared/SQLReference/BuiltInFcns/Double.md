[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Double.html)

<a href="" id="BuiltInFcns.Double"></a>[]()DOUBLE
=================================================

The <span class="CodeFont">DOUBLE</span> function returns a floating-point number corresponding to a:

-   number if the argument is a numeric expression
-   character string representation of a number if the argument is a string expression

Numeric to Double

``` FcnSyntax
DOUBLE [PRECISION] (NumericExpression ) 
```

NumericExpression

The argument is an expression that returns a value of any built-in numeric data type.

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span>value.

The result is the same value that would result if the argument were assigned to a double-precision floating-point column or variable.

Character String to Double

``` FcnSyntax
DOUBLE (StringExpression ) 
```

StringExpression

The argument can be of type [<span class="CodeFont">CHAR</span>](../DataTypes/Char.html) or [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html) in the form of a numeric constant. Leading and trailing blanks in argument are ignored.

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span>value.

The result is the same value that would result if the string was considered a constant and assigned to a double-precision floating-point column or variable.

Example

``` Example
splice> VALUES DOUBLE(84.4);
1
----------
84.4

1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)

 


