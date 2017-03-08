[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Min.html)

<a href="" id="BuiltInFcns.Min"></a>[]()MIN
===========================================

<span class="CodeFont">MIN</span> evaluates the minimum of an expression over a set of rows. You can use it as an [aggregate function](Intro.WindowAggregrateFcns.html) or as a [window (analytic) function](Intro.WindowAggregrateFcns.html).

Syntax

``` FcnSyntax
MIN ( [ DISTINCT | ALL ] Expression )
```

DISTINCT

If this qualifier is specified, duplicates are eliminated.

<span class="ItalicFont">ALL</span>

If this qualifier is specified, all duplicates are retained. This is the default value.

Expression

An expression that evaluates to a numeric data type: [<span class="CodeFont">DECIMAL</span>](../DataTypes/Decimal.html), [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html), [<span class="CodeFont">FLOAT</span>](../DataTypes/Float.html), [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html), [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html), [<span class="CodeFont">NUMERIC</span>](../DataTypes/Numeric.html), [<span class="CodeFont">REAL</span>](../DataTypes/Real.html), or [<span class="CodeFont">SMALLINT</span>](../DataTypes/SmallInt.html).

The expression can contain multiple column references or expressions, but it cannot contain another aggregate or subquery, and it must evaluate to an ANSI SQL numeric data type. This means that you can call methods that evaluate to ANSI SQL data types.

If an expression evaluates to <span class="CodeFont">NULL</span>, the aggregate skips that value.

Usage

Only one <span class="CodeFont">DISTINCT</span> aggregate expression per <span class="ItalicFont">Expression</span> is allowed. For example, the following query is not valid:

``` Example
   --- Not a valid query:
SELECT COUNT (DISTINCT flying_time),
              MIN (DISTINCT miles)
 FROM Flights;
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span> Since duplicate values do not change the computation of the minimum value, the <span class="CodeFont">DISTINCT</span> and <span class="CodeFont">ALL</span> qualifiers have no impact on this function.

The <span class="ItalicFont">Expression</span> can contain multiple column references or expressions, but it cannot contain another aggregate or subquery. It must evaluate to a built-in data type. You can therefore call methods that evaluate to built-in data types. (For example, a method that returns a <span class="ItalicFont">java.lang.Integer</span> or <span class="ItalicFont">int</span> evaluates to an <span class="CodeFont">INTEGER</span>.) If an expression evaluates to <span class="CodeFont">NULL</span>, the aggregate skips that value.

Results

The resulting data type is the same as the expression on which it operates; it will never overflow.

The comparison rules for the <span class="ItalicFont">Expression's</span> type determine the resulting minimum value. For example, if you supply a [<span class="CodeFont">CHAR</span>](../DataTypes/Char.html) or [<span class="CodeFont">VARCHAR</span>](../DataTypes/Varchar.html) argument, the number of blank spaces at the end of the value can affect how the minimum value is evaluated: if the values <span class="CodeFont">'z'</span> and <span class="CodeFont">'z '</span> are both stored in a column, you cannot control which one will be returned as the minimum, because blank spaces are ignored for character comparisons.

Examples

``` Example
splice> SELECT MIN (BirthDate) FROM Players;
1
----------
1975-07-13
```

This example finds the minimum number of walks and strikeouts by any pitcher in the database:

``` Example
splice> SELECT MIN(Walks) "Walks", Min(Strikeouts) "Strikeouts" 
   FROM Pitching JOIN Players on Pitching.ID=Players.ID 
   WHERE Position='P';
Walks |Strik&
-------------
1     |1     

1 row selected
```

Analytic Example

The following shows the homeruns hit by all batters who hit more than 10, compared to the least number of Homeruns by a player who hit 10 or more on his team:

``` Example
splice> SELECT Team, DisplayName, HomeRuns, 
   MIN(HomeRuns) OVER (PARTITION BY Team ORDER BY HomeRuns 
   ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) "Least" 
   FROM Players JOIN Batting ON Players.ID=Batting.ID
   WHERE HomeRuns > 10
   ORDER BY Team, HomeRuns DESC;
TEAM      |DISPLAYNAME             |HOMER&|Least 
--------------------------------------------------
Cards     |Mitch Canepa            |28    |11    
Cards     |Jonathan Pearlman       |17    |11    
Cards     |Roger Green             |17    |11    
Cards     |Michael Rastono         |13    |11    
Cards     |Jack Hellman            |13    |11    
Cards     |Kelly Wacherman         |11    |11    
Giants    |Bob Cranker             |21    |12    
Giants    |Buddy Painter           |19    |12    
Giants    |Billy Bopper            |18    |12    
Giants    |Mitch Duffer            |12    |12    

10 rows selected
```

See Also

-   [Window and Aggregate functions](Intro.WindowAggregrateFcns.html)
-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">AVG</span>](Avg.html) function
-   [<span class="CodeFont">COUNT</span>](Count.html) function
-   [<span class="CodeFont">MAX</span>](Max.html) function
-   [<span class="CodeFont">SUM</span>](Sum.html) function
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause

 


