[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Exp.html)

<a href="" id="BuiltInFcns.Exp"></a>[]()EXP
===========================================

The <span class="CodeFont">EXP</span> function returns <span class="CodeFont">e</span> raised to the power of the specified number. The constant <span class="CodeFont">e</span> is the base of the natural logarithms.

Syntax

``` FcnSyntax
EXP ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number that specifies the exponent to which you want to raise <span class="CodeFont">e</span>.

Example

``` Example
splice> VALUES EXP(1.234);
1
----------
3.43494186080076

1 row selected
```

Results

The data type of the result is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


