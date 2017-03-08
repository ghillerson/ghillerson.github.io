[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/InitCap.html)

[]()INITCAP
===========

The <span class="CodeFont">INITCAP</span> function converts the first letter of each word in a string to uppercase, and converts any remaining characters in each word to lowercase. Words are delimited by white space characters, or by characters that are not alphanumeric.

Syntax

``` FcnSyntax
INITCAP( charExpression );
```

charExpression

The string to be converted. This can be a <span class="CodeFont">CHAR</span> or <span class="CodeFont">VARCHAR</span> data type, or another type that gets implicitly converted.

Results

The returned string has the same data type as the input <span class="CodeFont">charExpression</span>.

Examples

``` Example
splice> VALUES( INITCAP('this is a test') );
1 
---------------------------------------------------------------------
This Is A Test
1 row selected

splice> VALUES( INITCAP('tHIS iS a test') );
1 
---------------------------------------------------------------------
This Is A Test
1 row selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Concatenation](Concatenation.html) operator
-   [<span class="CodeFont">INSTR</span>](Instr.html) function
-   [<span class="CodeFont">LCASE</span>](LCase.html) function
-   [<span class="CodeFont">LENGTH</span>](Length.html) function
-   [<span class="CodeFont">LOCATE</span>](Locate.html) function
-   [<span class="CodeFont">LTRIM</span>](LTrim.html) function
-   <span class="CodeFont">[REGEX\_LIKE](RegexpLike.html)</span> operator
-   [<span class="CodeFont">REPLACE</span>](Replace.html) function
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


