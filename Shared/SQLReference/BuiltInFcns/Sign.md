[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Sign.html)

<a href="" id="BuiltInFcns.Sign"></a>[]()SIGN
=============================================

The <span class="CodeFont">SIGN</span> function returns the sign of the specified number.

Syntax

``` FcnSyntax
SIGN ( number )
```

number

A [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) number that specifies the value whose sign you want.

Results

The data type of the returned value is [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html):.

-   If the specified number is <span class="CodeFont">NULL</span>, the result of this function is <span class="CodeFont">NULL</span>.
-   If the specified number is zero (<span class="CodeFont">0</span>), the result of this function is zero (<span class="CodeFont">0</span>).
-   If the specified number is greater than zero (<span class="CodeFont">0</span>), the result of this function is plus one (<span class="CodeFont">+1</span>).
-   If the specified number is less than zero (<span class="CodeFont">0</span>), the result of this function is minus one (<span class="CodeFont">-1</span>).

Example

``` Example
splice> VALUES( SIGN(84.4), SIGN(-85.5), SIGN(0), SIGN(NULL) );
1          |2          |3          |4          
-----------------------------------------------
1          |-1         |0          |NULL       

1 row selected
```

See Also

-   [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html) data type

 


