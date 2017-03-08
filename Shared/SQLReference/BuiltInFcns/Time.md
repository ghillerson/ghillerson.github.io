[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Time.html)

<a href="" id="BuiltInFcns.Time"></a>[]()TIME
=============================================

The <span class="CodeFont">TIME</span> function returns a time from a value.

Syntax

``` FcnSyntax
TIME ( expression )
```

expression

An expression that can be any of the following:

-   A [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) value
-   A [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) value
-   A valid string representation of a time or timestamp

Results

The returned result is governed by the following rules:

-   If the argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>; if the argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span>value.
-   If the argument is a time, the result is that time value.
-   If the argument is a timestamp, the result is the time part of the timestamp.
-   If the argument is a string, the result is the time represented by the string.

Syntax

``` FcnSyntax
TIME ( expression )
```

Example

``` Example
splice> VALUES TIME( CURRENT_TIMESTAMP );
1
--------
18:53:13

1 row selected
```

See Also

-   [<span class="CodeFont">TIME</span>](../DataTypes/Time.html) data type
-   [<span class="CodeFont">TIMESTAMP</span>](../DataTypes/TimeStamp.html) data type

 


