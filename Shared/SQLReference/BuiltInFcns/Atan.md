[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Atan.html)

<a href="" id="BuiltInFcns.Atan"></a>[]()ATAN
=============================================

The <span class="CodeFont">ATAN</span> function returns the arc tangent of a specified number.

Syntax

``` FcnSyntax
ATAN ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number that specifies the tangent, in radians, of the angle that you want.

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number. The returned value, in radians, is in the range <span class="CodeFont">pi/2</span> to <span class="CodeFont">pi/2</span>.

-   If the specified number is <span class="CodeFont">NULL</span>, the result of this function is <span class="CodeFont">NULL</span>.
-   If the specified number is zero (<span class="CodeFont">0</span>), the result of this function is zero with the same sign as the specified number.
-   If the absolute value of the specified number is greater than 1, an exception is returned that indicates that the value is out of range (SQL state 22003).

Example

``` Example
splice> VALUES ATAN(0.5);
1
----------
0.46364760900008061

1 row selected
```

See Also

-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type
-   [<span class="CodeFont">ACOS</span>](Acos.html) function
-   [<span class="CodeFont">ASIN</span>](Asin.html) function
-   [<span class="CodeFont">ATAN2</span>](Atan2.html) function
-   [<span class="CodeFont">COS</span>](Cos.html) function
-   [<span class="CodeFont">COSH</span>](Cosh.html) function
-   [<span class="CodeFont">COT</span>](Cot.html) function
-   [<span class="CodeFont">DEGREES</span>](Degrees.html) function
-   [<span class="CodeFont">RADIANS</span>](Radians.html) function
-   [<span class="CodeFont">SIN</span>](Sin.html) function
-   [<span class="CodeFont">SINH</span>](Sinh.html) function
-   [<span class="CodeFont">TAN</span>](Tan.html) function
-   [<span class="CodeFont">TANH</span>](Tanh.html) function

 


