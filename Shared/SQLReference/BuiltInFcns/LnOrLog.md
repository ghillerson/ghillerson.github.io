[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/LnOrLog.html)

<a href="" id="BuiltInFcns.LnOrLog"></a>[]()LN or []()LOG
=========================================================

The <span class="CodeFont">LN</span> and <span class="CodeFont">LOG</span> functions return the natural logarithm (base <span class="CodeFont">e</span>) of the specified number.

Syntax

``` FcnSyntax
LN ( number )
LOG ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number that is greater than zero (<span class="CodeFont">0</span>).

Example

``` Example
splice> VALUES( LOG(84.4), LN(84.4) );
1                  |2
--------------------------------------
4.435674016019115  |4.435674016019115

1 row selected
```

Results

The data type of the returned value is a [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number.

-   If the specified number is <span class="CodeFont">NULL</span>, the result of these functions is <span class="CodeFont">NULL</span>.
-   If the specified number is zero or a negative number, an exception is returned that indicates that the value is out of range (SQL state 22003).

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


