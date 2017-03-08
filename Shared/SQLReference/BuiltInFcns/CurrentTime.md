[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/CurrentTime.html)

<a href="" id="BuiltInFcns.CurrentTime"></a>[]()CURRENT\_TIME
=============================================================

<span class="CodeFont">CURRENT\_TIME</span> returns the current time.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>This function returns the same value if it is executed more than once in a single statement, which means that the value is fixed, even if there is a long delay between fetching rows in a cursor.

Syntax

``` FcnSyntax
CURRENT_TIME
```

or, alternately

``` FcnSyntax
CURRENT TIME
```

Results

A time value.

Examples

``` Example
splice> VALUES CURRENT_TIME;
1
--------
11:02:57

1 row selected
```

 


