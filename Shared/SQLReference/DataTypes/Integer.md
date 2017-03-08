[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Integer.html)

<a href="" id="DataTypes.Integer"></a>[]()INTEGER Data Type
===========================================================

The <span class="CodeFont">INTEGER</span> data type provides 4 bytes of storage for integer values.

Syntax

``` FcnSyntax
{ INTEGER | INT }
```

Corresponding Compile-Time Java Type

``` FcnSyntax
java.lang.Integer
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
INTEGER
```

Minimum Value

``` FcnSyntax
-2147483648  (java.lang.Integer.MIN_VALUE)
```

Maximum Value

``` FcnSyntax
2147483647 (java.lang.Integer.MAX_VALUE)
```

Usage Notes

When mixed with other data types in expressions, the resulting data type follows the rules shown in [Numeric type promotion in expressions](Intro.NumericTypes.html#NumericTypePromotion).

See also [Storing values of one numeric data type in columns of another numeric data type](Intro.NumericTypes.html#StoringValues).

Examples

``` Example
3453
425
```

 


