[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Sinh.html)

<a href="" id="BuiltInFcns.Sinh"></a>[]()SINH
=============================================

The <span class="CodeFont">SINH</span> function returns the hyperbolic sine of a specified number.

Syntax

``` FcnSyntax
SINH ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number that specifies the angle, in radians, for which you want the hyperbolic sine computed.

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

If <span class="ItalicFont">number</span> is <span class="CodeFont">NULL</span>, the result of the function is <span class="CodeFont">NULL</span>.

If <span class="ItalicFont">number</span> is <span class="CodeFont">0</span>, the result of the function is <span class="CodeFont">0</span>.

Example

``` Example
splice> VALUES SINH(84.4);
1
----------
2.2564425307671042E36

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
-   [<span class="CodeFont">RADIANS</span>](Radians.html) function
-   [<span class="CodeFont">SIN</span>](Sin.html) function
-   [<span class="CodeFont">TAN</span>](Tan.html) function
-   [<span class="CodeFont">TANH</span>](Tanh.html) function

 


