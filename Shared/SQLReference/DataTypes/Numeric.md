[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Numeric.html)

<a href="" id="DataTypes.Numeric"></a>[]()NUMERIC Data Type
===========================================================

<span class="CodeFont">NUMERIC</span> is a synonym for the <span class="CodeFont">[DECIMAL](Decimal.html)</span> data type and behaves the same way. The documentation below is a mirror of the documentation for the <span class="CodeFont">DECIMAL</span> data type.

<span class="CodeFont">NUMERIC</span> provides an exact numeric in which the precision and scale can be arbitrarily sized. You can specify the <span class="ItalicFont">precision</span> (the total number of digits, both to the left and the right of the decimal point) and the <span class="ItalicFont">scale</span> (the number of digits of the fractional component). The amount of storage required depends on the precision you specify.

Syntax

``` FcnSyntax
NUMERIC [(precision [, scale ])]
```

precision

Must be between <span class="CodeFont">1</span> and <span class="CodeFont">31</span>. If not specified, the default precision is <span class="CodeFont">5</span>.

scale

Must be less than or equal to the precision. If not specified, the default scale is <span class="CodeFont">0</span>.

Usage Notes

Here are several notes about using the <span class="CodeFont">NUMERIC</span> data type:

-   An attempt to put a numeric value into a <span class="CodeFont">NUMERIC</span> is allowed as long as any non-fractional precision is not lost. When truncating trailing digits from a <span class="CodeFont">NUMERIC</span> value, Splice Machine rounds down. For example:
    ``` Example
      -- this cast loses only fractional precision
    values cast (1.798765 AS numeric(5,2));
    1
    --------
    1.79
        -- this cast does not fit:
    values cast (1798765 AS numeric(5,2));
    ERROR 22003: The resulting value is outside the range for the data type DECIMAL/NUMERIC(5,2).
    ```

-   When mixed with other data types in expressions, the resulting data type follows the rules shown in [Numeric type promotion in expressions](Intro.NumericTypes.html#NumericTypePromotion). See also [Storing values of one numeric data type in columns of another numeric data type](Intro.NumericTypes.html#StoringValues).
-   When two numeric values are mixed in an expression, the scale and precision of the resulting value follow the rules shown in [Scale for decimal arithmetic](Intro.NumericTypes.html#Scale).
-   Integer constants too big for <span class="CodeFont">BIGINT</span> are made <span class="CodeFont">NUMERIC</span> constants.

Corresponding Compile-time Java Type

``` FcnSyntax
java.math.BigDecimal
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
NUMERIC
```

Examples

``` Example
VALUES 123.456;
VALUES 0.001;
```

 


