[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Length.html)

<a href="" id="BuiltInFcns.Length"></a>[]()LENGTH
=================================================

The <span class="CodeFont">LENGTH</span> function returns the number of characters in a character string expression or bit string expression.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span> Since all built-in data types are implicitly converted to strings, this function can act on all built-in data types.

Syntax

``` FcnSyntax
LENGTH ( { CharacterExpression | BitExpression } )
```

CharacterExpression

A character string expression.

BitExpression

A bit string expression.

Results

The result data type is an integer value.

Examples

The following three examples show the values returned by the LENGTH function for string, integer, and bit string values.

``` Example
splice> SELECT DisplayName, LENGTH(DisplayName) "NameLen" 
   FROM Players 
   WHERE ID < 11 
   ORDER BY "NameLen";
DISPLAYNAME             |NameLen    
------------------------------------
Greg Brown              |10         
John Purser             |11         
Bob Cranker             |11         
Billy Bopper            |12         
Mitch Duffer            |12         
Jason Minman            |12         
Buddy Painter           |13         
Norman Aikman           |13         
Alex Paramour           |13         
Harry Pennello          |14         

10 rows selected


splice> SELECT ID, 
   LENGTH(CAST(ID AS SMALLINT)) "SMALLINT", 
   LENGTH(CAST(ID AS INT)) "INT", 
   LENGTH(CAST(ID AS BIGINT)) "BIGINT", 
   LENGTH(CAST(ID AS DECIMAL)) "DECIMAL5", 
   LENGTH(CAST(ID AS DECIMAL(15,10))) "DECIMAL15", 
   LENGTH(CAST(ID AS DECIMAL(30,25))) "DECIMAL30" 
   FROM Players 
   WHERE ID<11;
ID    |SMALLINT   |INT        |BIGINT     |DECIMAL5   |DECIMAL15  |DECIMAL30
------------------------------------------------------------------------------
1     |2          |4          |8          |3          |8          |16         
2     |2          |4          |8          |3          |8          |16         
3     |2          |4          |8          |3          |8          |16         
4     |2          |4          |8          |3          |8          |16         
5     |2          |4          |8          |3          |8          |16         
6     |2          |4          |8          |3          |8          |16         
7     |2          |4          |8          |3          |8          |16         
8     |2          |4          |8          |3          |8          |16         
9     |2          |4          |8          |3          |8          |16         
10    |2          |4          |8          |3          |8          |16         

10 rows selected


splice> VALUES LENGTH(X'FF'),
   LENGTH(X'FFFF'),
   LENGTH(X'FFFFFFFF'),
   LENGTH(X'FFFFFFFFFFFFFFFF');
-----------
1          
2          
4          
8          

4 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Concatenation](Concatenation.html) operator
-   [<span class="CodeFont">INITCAP</span>](InitCap.html) function
-   [<span class="CodeFont">INSTR</span>](Instr.html) function
-   [<span class="CodeFont">LCASE</span>](LCase.html) function
-   [<span class="CodeFont">LOCATE</span>](Locate.html) function
-   [<span class="CodeFont">LTRIM</span>](LTrim.html) function
-   <span class="CodeFont">[REGEX\_LIKE](RegexpLike.html)</span> operator
-   [<span class="CodeFont">REPLACE</span>](Replace.html) function
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


