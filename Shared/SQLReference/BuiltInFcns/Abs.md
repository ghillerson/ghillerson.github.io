[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Abs.html)

<a href="" id="BuiltInFcns.Abs"></a>[]()ABS or []()ABSVAL
=========================================================

<span class="CodeFont">ABS</span> or <span class="CodeFont">ABSVAL</span> returns the absolute value of a numeric expression.

Syntax

``` FcnSyntax
ABS(NumericExpression)
```

NumericExpression

A numeric expression; all built-in numeric types are supported: [<span class="CodeFont">DECIMAL</span>](../DataTypes/Decimal.html), [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html), [<span class="CodeFont">FLOAT</span>](../DataTypes/Float.html), [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html), [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html), [<span class="CodeFont">NUMERIC</span>](../DataTypes/Numeric.html), [<span class="CodeFont">REAL</span>](../DataTypes/Real.html), or [<span class="CodeFont">SMALLINT</span>](../DataTypes/SmallInt.html)

Results

The return type is the type of the input parameter.

Example

``` Example
splice> VALUES ABS(-3);
1
----------
3

1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.DataTypes.html)

 


