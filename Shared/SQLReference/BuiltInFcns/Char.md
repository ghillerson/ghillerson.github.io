[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Char.html)

<a href="" id="BuiltInFcns.Char"></a>[]()CHAR
=============================================

The <span class="CodeFont">CHAR</span> function returns a fixed-length character string representation. The representations are:

-   A character string, if the first argument is any type of character string.
-   A datetime value, if the first argument is a date, time, or timestamp.
-   A decimal number, if the first argument is a decimal number.
-   A double-precision floating-point number, if the first argument is a <span class="CodeFont">DOUBLE</span> or <span class="CodeFont">REAL</span>.
-   An integer number, if the first argument is a <span class="CodeFont">SMALLINT</span>, <span class="CodeFont">INTEGER</span>, or <span class="CodeFont">BIGINT</span>.

The first argument must be of a built-in data type.

The result of the <span class="CodeFont">CHAR</span> function is a fixed-length character string. If the first argument can be <span class="CodeFont">NULL</span>, the result can be <span class="CodeFont">NULL</span>. If the first argument is <span class="CodeFont">NULL</span>, the result is the <span class="CodeFont">NULL</span>value.

Character to character syntax

``` FcnSyntax
CHAR (CharacterExpression [, integer] ) 
```

CharacterExpression

An expression that returns a value that is <span class="CodeFont">CHAR</span>, <span class="CodeFont">VARCHAR</span>, <span class="CodeFont">LONG VARCHAR</span>, or <span class="CodeFont">CLOB</span> data type.

integer

The length attribute for the resulting fixed length character string. The value must be between 0 and 254.

> Results
>
> If the length of the character-expression is less than the length attribute of the result, the result is padded with blanks up to the length of the result.
>
> If the length of the character-expression is greater than the length attribute of the result, truncation is performed. A warning is returned unless the truncated characters were all blanks and the character-expression was not a long string (<span class="CodeFont">LONG VARCHAR</span> or <span class="CodeFont">CLOB</span>).

Integer to character syntax

``` FcnSyntax
CHAR (IntegerExpression ) 
```

IntegerExpression

An expression that returns a value that is an integer data type (either SMALLINT, INTEGER or BIGINT).

> Results
>
> The result is the character string representation of the argument in the form of an SQL integer constant. The result consists of n characters that are the significant digits that represent the value of the argument with a preceding minus sign if the argument is negative. It is left justified.
>
> -   If the first argument is a small integer: The length of the result is 6. If the number of characters in the result is less than 6, then the result is padded on the right with blanks to length 6.
> -   If the first argument is a large integer: The length of the result is 11. If the number of characters in the result is less than 11, then the result is padded on the right with blanks to length 11.
> -   If the first argument is a big integer: The length of the result is 20. If the number of characters in the result is less than 20, then the result is padded on the right with blanks to length 20.

Datetime to character syntax

``` FcnSyntax
CHAR (DatetimeExpression ) 
```

DatetimeExpression

An expression that is one of the following three data types:

| Type      | Description                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| DATE      | The result is the character representation of the date. The length of the result is 10.             |
| TIME      | The result is the character representation of the time. The length of the result is 8.              |
| TIMESTAMP | The result is the character string representation of the timestamp. The length of the result is 26. |

Decimal to character

``` FcnSyntax
CHAR (DecimalExpression ) 
```

DecimalExpression

An expression that returns a value that is a decimal data type.

If a different precision and scale is desired, you can use the <span class="CodeFont">DECIMAL</span> scalar function first to make the change.

Floating point to character syntax

``` FcnSyntax
CHAR (FloatingPointExpression ) 
```

FloatingPointExpression

An expression that returns a value that is a floating-point data type (<span class="CodeFont">DOUBLE</span> or <span class="CodeFont">REAL</span>).

Example

Use the <span class="CodeFont">CHAR</span> function to return the values for <span class="CodeFont">PlateAppearances</span> (defined as smallint) as a fixed length character string:

``` Example
splice> SELECT CHAR(AtBats * 2) "DoubledAtBats"
  FROM Batting WHERE ID <= 10;
DoubledAtBats
--------------------
1246
1112
864
1122
1224
784
1102
446
744
548

10 rows selected
```

Since <span class="CodeFont">AtBats</span> is declared as <span class="CodeFont">SMALLINT</span> in our Examples database, each of the resulting values is padded with blank characters to make it 6 characters long.

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)

 


