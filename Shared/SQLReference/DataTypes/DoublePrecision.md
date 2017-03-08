[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/DoublePrecision.html)

<a href="" id="DataTypes.DoublePrecision"></a>[]()DOUBLE PRECISION
==================================================================

The <span class="CodeFont">DOUBLE PRECISION</span> data type provides 8-byte storage for numbers using IEEE floating-point notation. <span class="CodeFont">DOUBLE</span> can be used synonymously with <span class="CodeFont">DOUBLE PRECISION</span>, and the documentation for this topic is identical to the documentation for the <span class="CodeFont">[DOUBLE](Double.html)</span> topic.

Syntax

``` FcnSyntax
DOUBLE PRECISION
```

or, alternately

``` FcnSyntax
DOUBLE
```

Usage Notes

Here are several usage notes for the <span class="CodeFont">DOUBLE</span>/<span class="CodeFont">DOUBLE PRECISION</span> data type:

-   The following range limitations apply:

    | Limit type                                                   | Limitation    |
    |--------------------------------------------------------------|---------------|
    | Smallest <span class="CodeFont">DOUBLE</span> value          | -1.79769E+308 |
    | Largest <span class="CodeFont">DOUBLE</span> value           | 1.79769E+308  |
    | Smallest positive <span class="CodeFont">DOUBLE</span> value | 2.225E-307    |
    | Largest negative <span class="CodeFont">DOUBLE</span> value  | -2.225E-307   |

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>These limits are different from the java.lang.Double Java type limits

-   An exception is thrown when any double value is calculated or entered that is outside of these value ranges. Arithmetic operations <span class="BoldFont">do not</span> round their resulting values to zero. If the values are too small, you will receive an exception.
-   Numeric floating point constants are limited to a length of 30 characters.
    ``` Example
       -- this example will fail because the constant is too long:
    values 01234567890123456789012345678901e0;
    ```

-   When mixed with other data types in expressions, the resulting data type follows the rules shown in [Numeric type promotion in expressions](Intro.NumericTypes.html#NumericTypePromotion). See also [Storing values of one numeric data type in columns of another numeric data type](Intro.NumericTypes.html#StoringValues).

Corresponding Compile-time Java Type

``` FcnSyntax
java.lang.Double
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
DOUBLE
```

Examples

``` Example
3421E+09
425.43E9
9E-10
4356267544.32333E+30
```

 


