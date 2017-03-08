[Open topic with navigation](../../../index.html#Shared/SQLReference/DataTypes/LongVarchar.html)

<a href="" id="DataTypes.LongVarchar"></a>[]()LONG VARCHAR
==========================================================

The <span class="CodeFont">LONG VARCHAR</span> type allows storage of character strings with a maximum length of 32,670 characters. It is almost identical to <span class="CodeFont">[VARCHAR](Varchar.html)</span>, except that you cannot specify a maximum length when creating columns of this type.

Syntax

``` FcnSyntax
LONG VARCHAR
```

Corresponding Compile-time Java Type

``` FcnSyntax
java.lang.String
```

JDBC Metadata Type (java.sql.Types)

``` FcnSyntax
LONGVARCHAR
```

Usage Notes

When you are converting from Java values to SQL values, no Java type corresponds to <span class="CodeFont">LONG VARCHAR</span>.

 


