[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Random.html)

<a href="" id="BuiltInFcns.Random"></a>[]()RANDOM
=================================================

The <span class="CodeFont">RANDOM</span> function returns a random number.

The <span class="CodeFont">RANDOM</span> function returns a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number with positive sign, greater than or equal to zero (<span class="CodeFont">0</span>), and less than one (<span class="CodeFont">1.0</span>), given an [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html) seed number.

Syntax

``` FcnSyntax
RANDOM()
```

Example

``` Example
splice> VALUES RANDOM();
1
----------
0.2826393098638572

1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


