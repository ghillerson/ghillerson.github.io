[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/LCase.html)

<a href="" id="BuiltInFcns.LCase"></a>[]()LCASE or []()LOWER
============================================================

<span class="CodeFont">LCASE</span> or <span class="CodeFont">LOWER</span> returns a string in which all alphabetic characters in the input character expression have been converted to lowercase.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="CodeFont">LOWER</span> and <span class="CodeFont">LCASE</span> follow the database locale.

Syntax

``` FcnSyntax
LCASE or LOWER ( CharacterExpression ) 
```

CharacterExpression

A [<span class="CodeFont">CHAR</span>](../DataTypes/Char.html), [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html), or [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html) data type, or any built-in type that is implicitly converted to a string (but not a bit expression).

Results

The data type of the result is as follows:

-   If the <span class="ItalicFont">CharacterExpression</span> evaluates to <span class="CodeFont">NULL</span>, this function returns <span class="CodeFont">NULL</span>.
-   If the <span class="ItalicFont">CharacterExpression</span> is of type [<span class="CodeFont">CHAR</span>](../DataTypes/Char.html), the return type is [<span class="CodeFont">CHAR</span>](../DataTypes/Char.html).
-   If the <span class="ItalicFont">CharacterExpression</span> is of type [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html), the return type is [<span class="CodeFont">LONG VARCHAR</span>](../DataTypes/LongVarchar.html).
-   Otherwise, the return type is [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html).

The length and maximum length of the returned value are the same as the length and maximum length of the parameter.

Examples

``` Example
splice> SELECT LCASE(DisplayName) 
   FROM Players 
   WHERE ID < 11;
1                       
------------------------
buddy painter           
billy bopper            
john purser             
bob cranker             
mitch duffer            
norman aikman           
alex paramour           
harry pennello          
greg brown              
jason minman            

10 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Concatenation](Concatenation.html) operator
-   [<span class="CodeFont">INITCAP</span>](InitCap.html) function
-   [<span class="CodeFont">INSTR</span>](Instr.html) function
-   [<span class="CodeFont">LENGTH</span>](Length.html) function
-   [<span class="CodeFont">LOCATE</span>](Locate.html) function
-   [<span class="CodeFont">LTRIM</span>](LTrim.html) function
-   <span class="CodeFont">[REGEX\_LIKE](RegexpLike.html)</span> operator
-   [<span class="CodeFont">REPLACE</span>](Replace.html) function
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


