[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Trim.html)

<a href="" id="BuiltInFcns.Trim"></a>[]()TRIM
=============================================

The <span class="CodeFont">TRIM</span> function that takes a character expression and returns that expression with leading and/or trailing pad characters removed. Optional parameters indicate whether leading, or trailing, or both leading and trailing pad characters should be removed, and specify the pad character that is to be removed.

Syntax

``` FcnSyntax
TRIM( [ trimOperands ] trimSource)
```

trimOperands

``` FcnSyntax
{  { trimType [trimCharacter]  FROM
  |  trimCharacter FROM
}
```

trimCharacter

A character expression that specifies which character to trim from the source. If this is specified, it must evaluate to either <span class="CodeFont">NULL</span> or to a character string whose length is exactly one. If left unspecified, it defaults to the space character (<span class="CodeFont">' '</span>).

trimType

``` FcnSyntax
{LEADING | TRAILING | BOTH}
```

If this value is not specified, the default value of <span class="CodeFont">BOTH</span> is used.

trimSource

The character expression to be trimmed

Results

If either <span class="ItalicFont">trimCharacter</span> or <span class="ItalicFont">trimSource</span> evaluates to <span class="CodeFont">NULL</span>, the result of the <span class="CodeFont">TRIM</span> function is <span class="CodeFont">NULL</span>. Otherwise, the result of the <span class="CodeFont">TRIM</span> function is defined as follows:

-   If <span class="ItalicFont">trimType</span> is <span class="CodeFont">LEADING</span>, the result will be the <span class="ItalicFont">trimSource</span> value with all leading occurrences of <span class="ItalicFont">trimCharacter</span> removed.
-   If <span class="ItalicFont">trimType</span> is <span class="CodeFont">TRAILING</span>, the result will be the <span class="ItalicFont">trimSource</span> value with all trailing occurrences of <span class="ItalicFont">trimCharacter</span>removed.
-   If <span class="ItalicFont">trimType</span> is <span class="CodeFont">BOTH</span>, the result will be the <span class="ItalicFont">trimSource</span> value with all leading AND trailing occurrences of <span class="ItalicFont">trimCharacter</span>removed.

If <span class="ItalicFont">trimSource</span>'s data type is [<span class="CodeFont">CHAR</span>](../DataTypes/Char.html) or [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html), the return type of the <span class="CodeFont">TRIM</span> function will be [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html). Otherwise the return type of the <span class="CodeFont">TRIM</span> function will be [<span class="CodeFont">CLOB</span>](../DataTypes/Clob.html).

Examples

``` Example
splice> VALUES TRIM('      Space Case   ');
1
-----------
Space Case  --- This is the string 'Space Case'

splice> VALUES TRIM(BOTH ' ' FROM '      Space Case   ');
1
-----------
Space Case  --- This is the string 'Space Case'

splice> VALUES TRIM(TRAILING ' ' FROM '     Space Case     ');
1
-----------
     Space Case --- This is the string '     Space Case'

splice> VALUES TRIM(CAST NULL AS CHAR(1) FROM '     Space Case     ');
1
-----------
NULL

splice> VALUES TRIM('o' FROM 'VooDoo');
1
----------
VooD

   -- results in an error because trimCharacter can only be 1 character
splice> VALUES TRIM('Do' FROM 'VooDoo');
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Concatenation](Concatenation.html) operator
-   [<span class="CodeFont">INITCAP</span>](InitCap.html) function
-   [<span class="CodeFont">INSTR</span>](Instr.html) function
-   [<span class="CodeFont">LCASE</span>](LCase.html) function
-   [<span class="CodeFont">LENGTH</span>](Length.html) function
-   [<span class="CodeFont">LOCATE</span>](Locate.html) function
-   [<span class="CodeFont">LTRIM</span>](LTrim.html) function
-   <span class="CodeFont">[REGEX\_LIKE](RegexpLike.html)</span> operator
-   [<span class="CodeFont">REPLACE</span>](Replace.html) function
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


