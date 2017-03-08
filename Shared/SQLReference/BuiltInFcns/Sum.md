[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Sum.html)

<a href="" id="BuiltInFcns.Sum"></a>[]()SUM
===========================================

<span class="CodeFont">SUM</span>returns the sum of values of an expression over a set of rows. You can use it as an [aggregate function](Intro.WindowAggregrateFcns.html) or as a [window (analytic) function](Intro.WindowAggregrateFcns.html).

The <span class="CodeFont">SUM</span> function function takes as an argument any numeric data type or any non-numeric data type that can be implicitly converted to a numeric data type. The function returns the same data type as the numeric data type of the argument.

Syntax

``` FcnSyntax
SUM ( [ DISTINCT | ALL ] Expression )
```

DISTINCT

If this qualifier is specified, duplicates are eliminated

If you specify <span class="CodeFont">DISTINCT</span> in the analytic version of <span class="CodeFont">SUM</span>, the <span class="CodeFont">[OVER](../Clauses/Over.html)</span> clause for your window function cannot include an <span class="CodeFont">ORDER BY</span> clause or a <span class="ItalicFont">frame clause</span>.

<span class="ItalicFont">ALL</span>

If this qualifier is specified, all duplicates are retained. This is the default value.

Expression

An expression that evaluates to a numeric data type: [<span class="CodeFont">DECIMAL</span>](../DataTypes/Decimal.html), [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html), [<span class="CodeFont">FLOAT</span>](../DataTypes/Float.html), [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html), [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html), [<span class="CodeFont">NUMERIC</span>](../DataTypes/Numeric.html), [<span class="CodeFont">REAL</span>](../DataTypes/Real.html), or [<span class="CodeFont">SMALLINT</span>](../DataTypes/SmallInt.html).

An <span class="ItalicFont">Expression</span> can contain multiple column references or expressions, but it cannot contain another aggregate or subquery.

If an <span class="ItalicFont">Expression</span>evaluates to <span class="CodeFont">NULL</span>, the aggregate skips that value.

Usage

The <span class="ItalicFont">Expression</span> can contain multiple column references or expressions, but it cannot contain another aggregate or subquery. It must evaluate to a built-in numeric data type. If an expression evaluates to <span class="CodeFont">NULL</span>, the aggregate skips that value.

Only one <span class="CodeFont">DISTINCT</span> aggregate expression per <span class="ItalicFont">Expression</span> is allowed. For example, the following query is not valid:

``` Example
   -- query not allowed
SELECT AVG (DISTINCT flying_time),
  SUM (DISTINCT miles)
  FROM Flights;
```

Note that specifying <span class="CodeFont">DISTINCT</span> can result in a different value, since a smaller number of values may be summed. For example, if a column contains the values 1, 1, 1, 1, and 2, <span class="CodeFont">SUM(col)</span> returns a greater value than <span class="CodeFont">SUM(DISTINCT col)</span>.

Results

The resulting data type is the same as the expression on which it operates (it might overflow).

Aggregate Examples

These queries compute the total of all salaries for all teams, and then the total for each individually.

``` Example
splice> SELECT SUM(Salary) FROM Salaries;
1                   
--------------------
277275362           

1 row selected
splice> SELECT SUM(Salary) FROM Salaries JOIN Players ON Salaries.ID=Players.ID WHERE Team='Cards';
1                   
--------------------
97007230            

1 row selected
splice> SELECT SUM(Salary) FROM Salaries JOIN Players ON Salaries.ID=Players.ID WHERE Team='Giants';
1                   
--------------------
180268132           

1 row selected
```

Analytic Example

This example computes the running total of salaries, per team, counting only the players who make at least $5 million in salary.

``` Example
splice> SELECT Team, DisplayName, Salary, 
   SUM(Salary) OVER(PARTITION BY Team ORDER BY Salary ASC
               ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) "Running Total" 
   FROM Players JOIN Salaries ON Players.ID=Salaries.ID 
   WHERE Salary>5000000 
   ORDER BY Team;
   
TEAM     |DISPLAYNAME             |SALARY              |RUNNING TOTAL        
---------------------------------------------------------------------
Cards    |Larry Lintos            |7000000             |7000000             
Cards    |Jack Hellman            |8300000             |15300000            
Cards    |James Grasser           |9375000             |24675000            
Cards    |Yuri Milleton           |15200000            |39875000            
Cards    |Mitch Hassleman         |17000000            |56875000            
Giants   |Jalen Ardson            |6000000             |60000000            
Giants   |Steve Raster            |6000000             |12000000            
Giants   |Marcus Bamburger        |6950000             |18950000            
Giants   |Mark Briste             |8000000             |26950000            
Giants   |Jack Peepers            |9000000             |35950000            
Giants   |Alex Paramour           |10250000            |46200000            
Giants   |Thomas Hillman          |12000000            |58200000            
Giants   |Buddy Painter           |17277777            |75477777            
Giants   |Tam Lassiter            |18000000            |93477777            
Giants   |Harry Pennello          |18500000            |111977777           
Giants   |Martin Cassman          |20833333            |132811110           

16 rows selected
```

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [Window and aggregate](Intro.WindowAggregrateFcns.html) functions
-   [<span class="CodeFont">AVG</span>](Avg.html) function
-   [<span class="CodeFont">COUNT</span>](Count.html) function
-   [<span class="CodeFont">MAX</span>](Max.html) function
-   [<span class="CodeFont">MIN</span>](Min.html) function
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause
-   <span class="ItalicFont">[Using Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html)</span> in the <span class="ItalicFont">Developer Guide</span>.

 


