[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Second.html)

<a href="" id="BuiltInFcns.Second"></a>[]()SECOND
=================================================

The <span class="CodeFont">SECOND</span> function returns the seconds part of a value.

Syntax

``` FcnSyntax
SECOND( expression )
```

expression

An expression that can be any of the following:

-   A [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) value
-   A [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) value
-   A valid string representation of a time or timestamp that is not a [<span class="CodeFont">CLOB</span>](../DataTypes/Clob.html) or [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html) value.

Results

The returned result is an integer value in the range 0 to 59.

If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span>value.

Example

``` Example
splice> VALUES( NOW(), HOUR(NOW), MINUTE(NOW), SECOND(NOW) );
1                            |2          |3          |4                     
----------------------------------------------------------------------------
2015-11-12 17:48:55.217      |17         |48         |55.217                

1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) data value
-   [<span class="CodeFont">HOUR</span>](Hour.html) function
-   [<span class="CodeFont">MINUTE</span>](Minute.html) function
-   [<span class="CodeFont">TIMESTAMP</span>](TimeStamp.html) function
-   [<span class="CodeFont">TIMESTAMPADD</span>](TimeStampAdd.html) function
-   [<span class="CodeFont">TIMESTAMPDIFF</span>](TimeStampDiff.html) function

 


