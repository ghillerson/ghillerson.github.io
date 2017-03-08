[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Atan2.html)

<a href="" id="BuiltInFcns.Atan2"></a>[]()ATAN2
===============================================

The <span class="CodeFont">ATAN2</span> function returns the arctangent, in radians, of the quotient of the two arguments.

Syntax

``` FcnSyntax
ATAN2 ( y, x )
```

y

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

x

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

Results

<span class="CodeFont">ATAN2</span> returns the arc tangent of <span class="ItalicFont">y</span>/<span class="ItalicFont">x</span> in the range -<span class="ItalicFont">pi</span> to <span class="ItalicFont">pi</span> radians, as a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html)number.

-   If either argument is <span class="CodeFont">NULL</span>, the result of the function is <span class="CodeFont">NULL</span>.
-   If the first argument is zero and the second argument is positive, the result of the function is zero.
-   If the first argument is zero and the second argument is negative, the result of the function is the double value closest to <span class="ItalicFont">pi</span>.
-   If the first argument is positive and the second argument is zero, the result is the double value closest to<span class="ItalicFont">pi</span>/2.
-   If the first argument is negative and the second argument is zero, the result is the double value closest to -<span class="ItalicFont">pi</span>/2.

Example

``` Example
splice> VALUES ATAN2(1, 0);
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
-   [<span class="CodeFont">COS</span>](Cos.html) function
-   [<span class="CodeFont">COSH</span>](Cosh.html) function
-   [<span class="CodeFont">COT</span>](Cot.html) function
-   [<span class="CodeFont">DEGREES</span>](Degrees.html) function
-   [<span class="CodeFont">RADIANS</span>](Radians.html) function
-   [<span class="CodeFont">SIN</span>](Sin.html) function
-   [<span class="CodeFont">SINH</span>](Sinh.html) function
-   [<span class="CodeFont">TAN</span>](Tan.html) function
-   [<span class="CodeFont">TANH</span>](Tanh.html) function

 


