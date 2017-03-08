[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/FirstValue.html)

[]()FIRST\_VALUE
================

<span class="CodeFont">FIRST\_VALUE</span> is a window function that returns the values of a specified expression that is evaluated at the first row of a window for the current row. This means that you can select a first value from a set of rows without having to use a self join.

Syntax

``` FcnSyntax
FIRST_VALUE ( expression [ {IGNORE | RESPECT} NULLS ] ) OVER ( overClause )
```

expression

The expression to evaluate; typically a column name or computation involving a column name.

IGNORE NULLS

If this optional qualifier is specified, <span class="CodeFont">NULL</span> values are ignored, and the first non-<span class="CodeFont">NULL</span> value is evaluated.

If you specify this and all values are <span class="CodeFont">NULL</span>, <span class="CodeFont">FIRST\_VALUE</span> returns <span class="CodeFont">NULL</span>.

RESPECT NULLS

This qualifier is the default behavior: it specifies that the first value is always returned, even if it is <span class="CodeFont">NULL</span>.

overClause

See the <span class="CodeFont">[OVER](../Clauses/Over.html)</span> clause documentation.

Usage Notes

Splice Machine recommends that you use the <span class="CodeFont">FIRST\_VALUE</span> function with the <span class="CodeFont">[ORDER BY](../Clauses/OrderBy.html)</span> clause to produce deterministic results.

Results

Returns value(s) resulting from the evaluation of the specified expression; the return type is of the same value type as the date stored in the column used in the expression..

-   <span class="CodeFont">FIRST\_VALUE</span> returns the first value in the set, unless that value is <span class="CodeFont">NULL</span> and you have specified the <span class="CodeFont">IGNORE NULLS</span> qualifier; if you've specified <span class="CodeFont">IGNORE NULLS</span>, this function returns the first non-<span class="CodeFont">NULL</span> value in the set.
-   If all values in the set are <span class="CodeFont">NULL</span>, <span class="CodeFont">FIRST\_VALUE</span> always returns <span class="CodeFont">NULL</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine always sorts <span class="CodeFont">NULL</span> values first in the results.

Examples

The following query finds all players with 10 or more HomeRuns, and compares each player's home run count with the lowest total within that group on his team:

``` Example
splice> SELECT Team, DisplayName, HomeRuns, 
   FIRST_VALUE(HomeRuns) OVER (PARTITION BY Team ORDER BY HomeRuns 
        ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) "Least" 
   FROM Players JOIN Batting ON Players.ID=Batting.ID
   WHERE HomeRuns > 10
   ORDER BY Team, HomeRuns DESC;
TEAM     |DISPLAYNAME             |HOMER&|Least 
-----------------------------------------------
Cards    |Mitch Canepa            |28    |11    
Cards    |Jonathan Pearlman       |17    |11    
Cards    |Roger Green             |17    |11    
Cards    |Michael Rastono         |13    |11    
Cards    |Jack Hellman            |13    |11    
Cards    |Kelly Wacherman         |11    |11    
Giants   |Bob Cranker             |21    |12    
Giants   |Buddy Painter           |19    |12    
Giants   |Billy Bopper            |18    |12    
Giants   |Mitch Duffer            |12    |12    

10 rows selected
```

See Also

-   [Window and Aggregate](Intro.WindowAggregrateFcns.html)functions
-   [<span class="CodeFont">AVG</span>](Avg.html) function
-   [<span class="CodeFont">COUNT</span>](Count.html) function
-   [<span class="CodeFont">LAG</span>](Lag.html) function
-   <span class="CodeFont">[LAST\_VALUE](LastValue.html)</span> function
-   <span class="CodeFont">[LEAD](Lead.html)</span> function
-   [<span class="CodeFont">MIN</span>](Min.html) function
-   [<span class="CodeFont">SUM</span>](Sum.html) function
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause
-   <span class="ItalicFont">[Using Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html)</span> in the <span class="ItalicFont">Developer Guide</span>.

 


