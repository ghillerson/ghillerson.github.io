[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Rand.html)

<a href="" id="BuiltInFcns.Rand"></a>[]()RAND
=============================================

The <span class="CodeFont">RAND</span> function returns a random number given a seed number

The <span class="CodeFont">RAND</span> function returns a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number with positive sign, greater than or equal to zero (<span class="CodeFont">0</span>), and less than one (<span class="CodeFont">1.0</span>), given an [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html) seed number.

Syntax

``` FcnSyntax
RAND( seed )
```

Example

``` Example
splice> VALUES RAND(13);
1
----------
0.7298032243379924

1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


