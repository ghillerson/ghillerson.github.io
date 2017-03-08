[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Locate.html)

<a href="" id="BuiltInFcns.Locate"></a>[]()LOCATE
=================================================

The <span class="CodeFont">LOCATE</span> function is used to search for a string (the <span class="ItalicFont">needle</span>) within another string (the <span class="ItalicFont">haystack</span>). If the desired string is found, <span class="CodeFont">LOCATE</span> returns the index at which it is found. If the desired string is not found, <span class="CodeFont">LOCATE</span> returns 0.

Syntax

``` FcnSyntax
LOCATE(CharacterExpression1, CharacterExpression2
        [, StartPosition] )
```

CharacterExpression1

A character expression that specifies the string to search <span class="BoldFont">for</span> in <span class="ItalicFont">CharacterExpression2</span>, sometimes called the needle.

CharacterExpression2

A character expression that specifies the string in which to search, sometimes called the haystack.

StartPosition

(Optional). Specifies the position in <span class="ItalicFont">CharacterExpression2</span> at which the search is to start. This defaults to the start of <span class="ItalicFont">CharacterExpression2</span>, which is the value <span class="CodeFont">1</span>.

Results

The return type for <span class="CodeFont">LOCATE</span> is an integer that indicates the index position within the second argument at which the first argument was first located. Index positions start with 1.

-   If the first argument is not found in the second argument, <span class="CodeFont">LOCATE</span> returns <span class="CodeFont">0</span>.
-   If the first argument is an empty string (<span class="CodeFont">''</span>), <span class="CodeFont">LOCATE</span> returns the value of the third argument (or <span class="CodeFont">1</span> if it was not provided), even if the second argument is also an empty string.
-   If a <span class="CodeFont">NULL</span> value is passed for either of the CharacterExpression arguments, <span class="CodeFont">NULL</span> is returned

Examples

``` Example
splice> SELECT DisplayName, LOCATE('Pa', DisplayName, 3) "Position" 
   FROM Players 
   WHERE (INSTR(DisplayName, 'Pa') > 0) 
   ORDER BY DisplayName;
DISPLAYNAME             |Position   
------------------------------------
Alex Paramour           |6          
Buddy Painter           |7          
Jeremy Packman          |8          
Pablo Bonjourno         |0          
Paul Kaster             |0          

5 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Concatenation](Concatenation.html) operator
-   [<span class="CodeFont">INITCAP</span>](InitCap.html) function
-   [<span class="CodeFont">INSTR</span>](Instr.html) function
-   [<span class="CodeFont">LCASE</span>](LCase.html) function
-   [<span class="CodeFont">LOCATE</span>](#) function
-   [<span class="CodeFont">LTRIM</span>](LTrim.html) function
-   <span class="CodeFont">[REGEX\_LIKE](RegexpLike.html)</span> operator
-   [<span class="CodeFont">REPLACE</span>](Replace.html) function
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


