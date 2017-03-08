[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Count.html)

<a href="" id="BuiltInFcns.Count"></a>[]()COUNT
===============================================

<span class="CodeFont">COUNT</span> returns the number of rows returned by the query. You can use it as an [aggregate function](Intro.WindowAggregrateFcns.html) or as a [window (analytic) function](Intro.WindowAggregrateFcns.html).

The <span class="CodeFont">COUNT(<span class="ItalicFont">Expression</span>)</span> version returns the number of row where <span class="ItalicFont">Expression</span> is not null. You can count either all rows, or only distinct values of <span class="ItalicFont">Expression</span>.

The <span class="CodeFont">COUNT(\*)</span> version returns all rows, including duplicates and nulls.

Syntax

``` FcnSyntax
COUNT( [ DISTINCT | ALL ] Expression )
```

DISTINCT

If this qualifier is specified, duplicates are eliminated from the count.

<span class="ItalicFont">ALL</span>

If this qualifier is specified, all duplicates are retained. This is the default value.

Expression

An expression that evaluates to a numeric data type: [<span class="CodeFont">DECIMAL</span>](../DataTypes/Decimal.html), [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html), [<span class="CodeFont">FLOAT</span>](../DataTypes/Float.html), [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html), [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html), [<span class="CodeFont">NUMERIC</span>](../DataTypes/Numeric.html), [<span class="CodeFont">REAL</span>](../DataTypes/Real.html), or [<span class="CodeFont">SMALLINT</span>](../DataTypes/SmallInt.html).

An <span class="ItalicFont">Expression</span> can contain multiple column references or expressions, but it cannot contain another aggregate or subquery.

If an <span class="ItalicFont">Expression</span>evaluates to <span class="CodeFont">NULL</span>, the aggregate skips that value.

Usage

Only one <span class="CodeFont">DISTINCT</span> aggregate expression per <span class="ItalicFont">[Expression](../Expressions/Select.html)</span> is allowed. For example, the following query is not valid:

``` Example
   -- query not allowed
SELECT COUNT (DISTINCT flying_time), SUM (DISTINCT miles)
  FROM Flights
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Note that specifying <span class="CodeFont">DISTINCT</span> can result in a different value, since a smaller number of values may be counted. For example, if a column contains the values 1, 1, 1, 1, and 2, <span class="CodeFont">COUNT(col)</span> returns a greater value than <span class="CodeFont">COUNT(DISTINCT col)</span>.

Results

The resulting data type is [BIGINT](../DataTypes/BigInt.html).

Aggregate Example

``` Example
splice> Select COUNT (Name) "Players", Team
   FROM Players
   GROUP BY Team
   HAVING COUNT(Team) > 1;
Players             |TEAM                                                            
-------------------------------------------------------------------------------------
46                  |Cards                                                           
48                  |Giants                                                          

2 rows selected
```

Analytic Example

The following example shows the product ID, quantity, and count of all rows from the beginning of the data window:

``` Example
splice> SELECT displayName, homeruns, 
   COUNT(*) OVER (ORDER BY HomeRuns ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
     as "Running Count" 
   FROM Players JOIN Batting ON Players.ID=Batting.ID 
   WHERE homeRuns > 5 
   ORDER BY "Running Count";
DISPLAYNAME             |HOMER&|Running Count      
----------------------------------------------------
Jeremy Packman          |6     |1                   
Jason Minman            |7     |2                   
Stan Post               |7     |3                   
John Purser             |8     |4                   
Harry Pennello          |9     |5                   
Kelly Wacherman         |11    |6                   
Mitch Duffer            |12    |7                   
Michael Rastono         |13    |8                   
Jack Hellman            |13    |9                   
Jonathan Pearlman       |17    |10                  
Roger Green             |17    |11                  
Billy Bopper            |18    |12                  
Buddy Painter           |19    |13                  
Bob Cranker             |21    |14                  
Mitch Canepa            |28    |15                  

15 rows selected
```

See Also

-   [<span>About Data Types</span>](../DataTypes/Intro.NumericTypes.html)
-   [Window and Aggregate Functions](Intro.WindowAggregrateFcns.html)
-   [<span class="CodeFont">AVG</span>](Avg.html) function
-   [<span class="CodeFont">MAX</span>](Max.html) function
-   [<span class="CodeFont">MIN</span>](Min.html) function
-   [<span class="CodeFont">SUM</span>](Sum.html) function
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause

 


