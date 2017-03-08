[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Lead.html)

[]()LEAD
========

<span class="CodeFont">LEAD</span> is a window function that returns the values of a specified expression that is evaluated at the specified offset number of rows after the current row in a window.

Syntax

``` FcnSyntax
LEAD ( expression [ , offset ] ) OVER ( overClause )
```

expression

The expression to evaluate; typically a column name or computation involving a column name.

offset

An integer value that specifies the offset (number of rows) from the current row at which you want the expression evaluated.

The default value is 1.

overClause

See the <span class="CodeFont">[OVER](../Clauses/Over.html)</span> clause documentation.

<span class="autonumber"><span class="noteAutoNum">RELEASE NOTE:  </span></span>Our current implementation of this function does not allow for specifying a default value, as is possible in some other database software.

Usage Notes

Splice Machine recommends that you use the <span class="CodeFont">LEAD</span> function with the <span class="CodeFont">[ORDER BY](../Clauses/OrderBy.html)</span> clause to produce deterministic results.

Results

Returns value(s) resulting from the evaluation of the specified expression; the return type is of the same value type as the date stored in the column used in the expression.

Examples

``` Example
splice> SELECT DisplayName, Position, Salary, 
   LEAD(SALARY) OVER (PARTITION BY Position ORDER BY Salary DESC) "NextLowerSalary"
   FROM Players JOIN Salaries ON Players.ID=Salaries.ID
   WHERE Salary>999999
   ORDER BY Position, Salary DESC;
DISPLAYNAME             |POS&|SALARY              |NextLowerSalary     
-----------------------------------------------------------------------
Billy Bopper            |1B  |3600000             |2379781             
Barry Morse             |1B  |2379781             |2000000             
Michael Rastono         |1B  |2000000             |NULL            
Craig McGawn            |3B  |4800000             |3750000             
Mitch Canepa            |3B  |3750000             |NULL                
Buddy Painter           |C   |17277777            |15200000            
Yuri Milleton           |C   |15200000            |NULL                
Alex Paramour           |CF  |10250000            |4125000             
Jeremy Johnson          |CF  |4125000             |1650000             
Pablo Bonjourno         |CF  |1650000             |NULL                
Mitch Hassleman         |LF  |17000000            |4000000             
Norman Aikman           |LF  |4000000             |1100000             
Trevor Imhof            |LF  |1100000             |NULL                
Greg Brown              |OF  |3600000             |NULL                
Martin Cassman          |P   |20833333            |18000000            
Tam Lassiter            |P   |18000000            |12000000            
Thomas Hillman          |P   |12000000            |9375000             
James Grasser           |P   |9375000             |9000000             
Jack Peepers            |P   |9000000             |7000000             
Larry Lintos            |P   |7000000             |6950000             
Marcus Bamburger        |P   |6950000             |6000000             
Jalen Ardson            |P   |6000000             |6000000             
Steve Raster            |P   |6000000             |5000000             
Sam Castleman           |P   |5000000             |4000000             
Randy Varner            |P   |4000000             |4000000             
Jason Lilliput          |P   |4000000             |3578825             
Mitch Lovell            |P   |3578825             |3500000             
Mitch Brandon           |P   |3500000             |3000000             
Robert Cohen            |P   |3000000             |2675000             
James Woegren           |P   |2675000             |2652732             
Sam Culligan            |P   |2652732             |2100000             
Yuri Piamam             |P   |2100000             |2000000             
Carl Vanamos            |P   |2000000             |1950000             
Alex Wister             |P   |1950000             |1200000             
Jan Bromley             |P   |1200000             |NULL                
Harry Pennello          |RF  |18500000            |8300000             
Jack Hellman            |RF  |8300000             |8000000             
Mark Briste             |RF  |8000000             |1000000             
Jason Minman            |RF  |1000000             |NULL                
Bob Cranker             |SS  |3175000             |1500000             
Jonathan Pearlman       |SS  |1500000             |NULL                
Joseph Arkman           |UT  |1450000             |NULL                

42 rows selected
```

See Also

-   [Window and Aggregate](Intro.WindowAggregrateFcns.html)functions
-   [<span class="CodeFont">AVG</span>](Avg.html) function
-   [<span class="CodeFont">COUNT</span>](Count.html) function
-   <span class="CodeFont">[FIRST\_VALUE](FirstValue.html)</span> function
-   <span class="CodeFont">[LAG](Lag.html)</span> function
-   <span class="CodeFont">[LAST\_VALUE](LastValue.html)</span> function
-   [<span class="CodeFont">MIN</span>](Min.html) function
-   [<span class="CodeFont">SUM</span>](Sum.html) function
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause
-   <span class="ItalicFont">[Using Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html)</span> in the <span class="ItalicFont">Developer Guide</span>.

 


