[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/SmallInt.html)

<a href="" id="DataTypes.SmallInt"></a>[]()SMALLINT
===================================================

The <span class="CodeFont">SMALLINT</span> data type provides 2 bytes of storage.

Syntax

``` FcnSyntax
SMALLINT
```

Corresponding Compile-time Java Type

``` FcnSyntax
java.lang.Short
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
SMALLINT
```

Usage Notes

Here are several usage notes for the <span class="CodeFont">SMALLINT</span> data type:

-   The minimum value is <span class="CodeFont">-32768</span> (<span class="CodeFont">java.lang.Short.MIN\_VALUE</span>).
-   The maximum value is <span class="CodeFont"> 32767</span> (<span class="CodeFont">java.lang.Short.MAX\_VALUE</span>).
-   When mixed with other data types in expressions, the resulting data type follows the rules shown in [Numeric type promotion in expressions](Intro.NumericTypes.html#NumericTypePromotion).
-   See also [Storing values of one numeric data type in columns of another numeric data type](Intro.NumericTypes.html#StoringValues).
-   Constants in the appropriate format always map to <span class="CodeFont">INTEGER</span> or <span class="CodeFont">BIGINT</span>, depending on their length.

 


