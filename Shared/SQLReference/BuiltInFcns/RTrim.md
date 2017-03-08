[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/RTrim.html)

<a href="" id="BuiltInFcns.RTrim"></a>[]()RTRIM
===============================================

<span class="CodeFont">RTRIM</span> removes blanks from the end of a character string expression.

Syntax

``` FcnSyntax
RTRIM(CharacterExpression)
```

CharacterExpression

A [<span class="CodeFont">CHAR</span>](../DataTypes/Char.html), [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html), or [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html) data type, any built-in type that is implicitly converted to a string.

Results

A character string expression. If the <span class="ItalicFont">CharacterExpression</span> evaluates to <span class="CodeFont">NULL</span>, this function returns <span class="CodeFont">NULL</span>.

Examples

``` Example
splice> VALUES RTRIM('     Space Case      ');
1
-------------
     Space Case --- This is the string '   Space Case'
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
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


