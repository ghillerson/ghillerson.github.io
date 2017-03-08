[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/CurrentTimestamp.html)

<a href="" id="BuiltInFcns.CurrentTimestamp"></a>[]()CURRENT\_TIMESTAMP
=======================================================================

<span class="CodeFont">CURRENT\_TIMESTAMP</span> returns the current timestamp.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span> This function returns the same value if it is executed more than once in a single statement, which means that the value is fixed, even if there is a long delay between fetching rows in a cursor.

Syntax

``` FcnSyntax
CURRENT_TIMESTAMP
```

or, alternately

``` FcnSyntax
CURRENT TIMESTAMP
```

Results

A timestamp value.

Examples

``` Example
splice> VALUES CURRENT_TIMESTAMP;
1
-----------------------------
2015-11-19 11:03:44.095

1 row selected
```

 


