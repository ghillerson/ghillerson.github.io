[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Degrees.html)

<a href="" id="BuiltInFcns.Degrees"></a>[]()DEGREES
===================================================

The <span class="CodeFont">DEGREES</span> function converts (approximately) a specified number from radians to degrees.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The conversion from radians to degrees is not exact. You should not expect <span class="CodeFont">DEGREES(ACOS(0.5))</span> to return exactly <span class="CodeFont">60.0</span>.

Syntax

``` FcnSyntax
DEGREES ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number that specifies the angle you want converted, in radians.

Example

``` Example
splice> VALUES DEGREES(ACOS(0.5));
1
----------
60.00000000000001

1 row selected
```

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

See Also

-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type
-   [<span class="CodeFont">ACOS</span>](Acos.html) function
-   [<span class="CodeFont">ASIN</span>](Asin.html) function
-   [<span class="CodeFont">ATAN</span>](Atan.html) function
-   [<span class="CodeFont">ATAN2</span>](Atan2.html) function
-   [<span class="CodeFont">COS</span>](Cos.html) function
-   [<span class="CodeFont">COSH</span>](Cosh.html) function
-   [<span class="CodeFont">COT</span>](Cot.html) function
-   [<span class="CodeFont">RADIANS</span>](Radians.html) function
-   [<span class="CodeFont">SIN</span>](Sin.html) function
-   [<span class="CodeFont">SINH</span>](Sinh.html) function
-   [<span class="CodeFont">TAN</span>](Tan.html) function
-   [<span class="CodeFont">TANH</span>](Tanh.html) function

 


