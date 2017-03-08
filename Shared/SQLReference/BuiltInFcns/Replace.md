[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Replace.html)

[]()REPLACE
===========

The <span class="CodeFont">REPLACE</span> function replaces all occurrences of a substring within a string and returns the new string.

Syntax

``` FcnSyntax
REPLACE(subjectStr, searchStr, replaceStr)
```

subjectStr

The string you want modified. This can be a literal string or a reference to a <span class="CodeFont">char</span> or <span class="CodeFont">varchar</span> value.

searchStr

The substring to replace within <span class="ItalicFont">subjectStr</span>. This can be a literal string or a reference to a <span class="CodeFont">char</span> or <span class="CodeFont">varchar</span> value.

replaceStr

The replacement substring. This can be a literal string or a reference to a <span class="CodeFont">char</span> or <span class="CodeFont">varchar</span> value.

Results

A string value.

Examples

The first examples shows the players on each team with averages greater than .300. The second example shows the result of replacing the team of those players with averages greater than 0.300 who play on one team (the Cards):

``` Example
splice> SELECT DisplayName, Average, Team
   FROM Players JOIN Batting on Players.ID=Batting.ID
   WHERE Average > 0.300 AND Games>50;
   
DISPLAYNAME             |AVERAGE  |TEAM 
------------------------------------------
Buddy Painter           |0.31777  |Giants
John Purser             |0.31151  |Giants
Kelly Tamlin            |0.30337  |Giants
Stan Post               |0.30472  |Cards

4 rows selected

splice> SELECT DisplayName, Average, 
    REPLACE(Team, 'Cards', 'Giants') "TRADED"
    FROM PLAYERS JOIN Batting ON Players.ID=Batting.ID 
    WHERE Team='Cards' AND Average > 0.300 AND Games > 50;
    
DISPLAYNAME             |AVERAGE  |TRADED
------------------------------------------
Stan Post               |0.30472  |Giants

1 row selected
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
-   [<span class="CodeFont">RTRIM</span>](RTrim.html) function
-   [<span class="CodeFont">SUBSTR</span>](Substr.html) function
-   [<span class="CodeFont">TRIM</span>](Trim.html) function
-   [<span class="CodeFont">UCASE</span>](UCase.html) function

 


