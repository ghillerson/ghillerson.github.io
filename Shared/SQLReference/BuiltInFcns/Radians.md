[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Radians.html)

<a href="" id="BuiltInFcns.Radians"></a>[]()RADIANS
===================================================

The <span class="CodeFont">RADIANS</span> function converts a specified number from degrees to radians.

The specified number is an angle measured in degrees, which is converted to an approximately equivalent angle measured in radians. The specified number must be a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The conversion from degrees to radians is not exact.

The data type of the returned value is a <span class="CodeFont">DOUBLE PRECISION</span> number.

Syntax

``` FcnSyntax
RADIANS ( number )
```

Example

``` Example
splice> VALUES RADIANS(90);
1
----------
1.5707963267948966

1 row selected
```

See Also

-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type
-   [<span class="CodeFont">ACOS</span>](Acos.html) function
-   [<span class="CodeFont">ASIN</span>](Asin.html) function
-   [<span class="CodeFont">ATAN</span>](Atan.html) function
-   [<span class="CodeFont">ATAN2</span>](Atan2.html) function
-   [<span class="CodeFont">COS</span>](Cos.html) function
-   [<span class="CodeFont">COSH</span>](Cosh.html) function
-   [<span class="CodeFont">COT</span>](Cot.html) function
-   [<span class="CodeFont">DEGREES</span>](Degrees.html) function
-   [<span class="CodeFont">SIN</span>](Sin.html) function
-   [<span class="CodeFont">SINH</span>](Sinh.html) function
-   [<span class="CodeFont">TAN</span>](Tan.html) function
-   [<span class="CodeFont">TANH</span>](Tanh.html) function

 


