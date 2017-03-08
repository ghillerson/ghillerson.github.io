[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Instr.html)

[]()INSTR
=========

The <span class="CodeFont">INSTR</span> function returns the index of the first occurrence of a substring in a string.

Syntax

``` FcnSyntax
INSTR(str, substring)
```

str

The string in which to search for the substring.

substring

The substring to search for.

Results

Returns the index in <span class="CodeFont">str</span> of the first occurrence of <span class="CodeFont">substring</span>.

The first index is <span class="CodeFont">1</span>.

If <span class="CodeFont">substring</span> is not found, <span class="CodeFont">INSTR</span> returns <span class="CodeFont">0</span>.

Examples

``` Example
splice> SELECT DisplayName, INSTR(DisplayName, 'Pa') "Position"  
   FROM Players 
   WHERE (INSTR(DisplayName, 'Pa') > 0) 
   ORDER BY DisplayName;
DISPLAYNAME             |Position   
------------------------------------
Alex Paramour           |6          
Buddy Painter           |7          
Jeremy Packman          |8          
Pablo Bonjourno         |1          
Paul Kaster             |1          

5 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Concatenation](Concatenation.html) operator
-   [<span class="CodeFont">INITCAP</span>](InitCap.html) function
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

 


