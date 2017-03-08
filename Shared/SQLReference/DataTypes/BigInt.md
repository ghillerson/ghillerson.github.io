[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/BigInt.html)

<a href="" id="DataTypes.BigInt"></a>[]()BIGINT
===============================================

The <span class="CodeFont">BIGINT</span> data type provides 8 bytes of storage for integer values.

Syntax

``` FcnSyntax
BIGINT
```

Corresponding Compile-time Java Type

``` FcnSyntax
java.lang.Long
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
BIGINT
```

Notes

Here are several usage notes for the <span class="CodeFont">BIGINT</span> data type:

-   The minimum value is <span class="CodeFont">-9223372036854775808</span> (<span class="CodeFont">java.lang.Long.MIN\_VALUE</span>)
-   The maximum value is <span class="CodeFont">9223372036854775807 </span> (<span class="CodeFont">java.lang.Long.MAX\_VALUE</span>)
-   When mixed with other data types in expressions, the resulting data type follows the rules shown in [Numeric type promotion in expressions](Intro.NumericTypes.html#NumericTypePromotion).
-   An attempt to put an integer value of a larger storage size into a location of a smaller size fails if the value cannot be stored in the smaller-size location. Integer types can always successfully be placed in approximate numeric values, although with the possible loss of some precision. <span class="CodeFont">BIGINTs</span> can be stored in <span class="CodeFont">DECIMALs</span> if the <span class="CodeFont">DECIMAL</span> precision is large enough for the value.

Example

``` Example
9223372036854775807
```

 


