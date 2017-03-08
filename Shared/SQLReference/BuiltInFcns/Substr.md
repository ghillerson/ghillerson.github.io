[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Substr.html)

<a href="" id="BuiltInFcns.Substr"></a>[]()SUBSTR
=================================================

The <span class="CodeFont">SUBSTR</span> function extracts and returns a portion of a character string or bit string expression, starting at the specified character or bit position. You can specify the number of characters or bits you want returned, or use the default length, which is to extract from the specified starting position to the end of the string.

Syntax

``` FcnSyntax
SUBSTR({ CharacterExpression },
        StartPosition [, LengthOfSubstring ] )
```

CharacterExpression

A <span class="CodeFont">CHAR</span>, <span class="CodeFont">VARCHAR</span>, or <span class="CodeFont">LONG VARCHAR</span> data type or any built-in type that is implicitly converted to a string (except a bit expression).

StartPosition

An integer expression; for character expressions, this is the starting character position of the returned substring. For bit expressions, this is the bit position of the returned substring.

The first character or bit has a <span class="ItalicFont">StartPosition</span> of 1. If you specify 0, Splice Machine assumes that you mean 1.

If the <span class="ItalicFont">StartPosition</span> is positive, it refers to the position from the start of the source expression (counting the first character as 1) to the beginning of the substring you want extracted. The <span class="ItalicFont">StartPosition</span> value cannot be a negative number.

LengthOfSubstring

An optional integer expression that specifies the length of the extracted substring; for character expressions, this is number of characters to return. For bit expressions, this is the number of bits to return.

If this value is not specified, then <span class="CodeFont">SUBSTR</span> extracts a substring of the expression from the <span class="ItalicFont">StartPosition</span> to the end of the source expression.

If <span class="ItalicFont">LengthOfString</span> is specified, <span class="CodeFont">SUBSTR</span> returns a <span class="CodeFont">VARCHAR</span> or <span class="CodeFont">VARBIT</span> of length <span class="ItalicFont">LengthOfString</span> starting at the <span class="ItalicFont">StartPosition</span>.

The <span class="CodeFont">SUBSTR</span> function returns an error if you specify a negative number for the parameter <span class="ItalicFont">LengthOfString</span>.

Results

For character string expressions, the result type is a [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html) value.

The length of the result is the maximum length of the source type.

Examples

The following query extracts the first four characters of each player's name, and then extracts the remaining characters:

``` Example
splice> SELECT DisplayName,
   SUBSTR(DisplayName, 1, 4) "1to4",
   SUBSTR(DisplayName, 4) "5ToEnd" 
   FROM Players 
   WHERE ID < 11;
DISPLAYNAME             |1To4|5ToEnd           
------------------------------------------------------
Buddy Painter           |Budd|dy Painter              
Billy Bopper            |Bill|ly Bopper               
John Purser             |John|n Purser                
Bob Cranker             |Bob | Cranker                
Mitch Duffer            |Mitc|ch Duffer               
Norman Aikman           |Norm|man Aikman              
Alex Paramour           |Alex|x Paramour              
Harry Pennello          |Harr|ry Pennello             
Greg Brown              |Greg|g Brown                 
Jason Minman            |Jaso|on Minman               

10 rows selected
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
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


