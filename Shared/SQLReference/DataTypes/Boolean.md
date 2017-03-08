[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/Boolean.html)

<a href="" id="DataTypes.Boolean"></a>[]()BOOLEAN
=================================================

The <span class="CodeFont">BOOLEAN</span> data type provides 1 byte of storage for logical values.

Syntax

``` FcnSyntax
BOOLEAN
```

Corresponding Compile-time Java Type

``` FcnSyntax
java.lang.Boolean
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
BOOLEAN
```

Usage Notes

Here are several usage notes for the <span class="CodeFont">BOOLEAN</span> data type:

-   The legal values are <span class="CodeFont">true</span>, <span class="CodeFont">false</span>, and <span class="CodeFont">null</span>.
-   <span class="CodeFont">BOOLEAN</span> values can be cast to and from character type values.
-   For comparisons and ordering operations, <span class="CodeFont">true</span> sorts higher than <span class="CodeFont">false</span>.

Examples

``` Example
values true;
values false;
values cast (null as boolean);
```

 


