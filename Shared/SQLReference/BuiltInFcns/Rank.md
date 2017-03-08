[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Rank.html)

[]()RANK()
==========

<span class="CodeFont">RANK()</span> is a <span class="ItalicFont">ranking function</span> that returns the rank of a value within the ordered partition of values defined by its <span class="CodeFont">OVER</span> clause. Ranking functions are a subset of [window functions](Intro.WindowAggregrateFcns.html).

Syntax

``` FcnSyntax
RANK() OVER ( overClause )
```

overClause

See the <span class="CodeFont">[OVER](../Clauses/Over.html)</span> clause documentation.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Ranking functions such as <span class="CodeFont">RANK</span> must include an <span class="CodeFont">[ORDER BY](../Clauses/OrderBy.html)</span> clause in the <span class="CodeFont">OVER</span> clause. This is because the ranking is calculated based on the ordering.

Results

The resulting data type is <span class="CodeFont">[BIGINT](../DataTypes/BigInt.html)</span>.

Usage

The <span class="CodeFont">RANK()</span> and <span class="CodeFont">[DENSE\_RANK()](DenseRank.html)</span> analytic functions are very similar. The difference shows up when there are multiple input rows that have the same ranking value. When that happens:

-   The <span class="CodeFont">RANK()</span> function can generate non-consecutive ranking result values: if values in the ranking column are the same, they receive the same rank; however, the next number in the ranking sequence is then skipped, which means that <span class="CodeFont">RANK</span> can return non-consecutive numbers.
-   The <span class="CodeFont">DENSE\_RANK()</span> function always returns consecutive rankings:if values in the ranking column are the same, they receive the same rank, and the next number in the ranking sequence is then used to rank the row or rows that follow.

Here's a simple example that shows the ranking produced by the two functions for input with duplicate values to illustrate that difference:

``` Example
-----------------------------
| Value | RANK | DENSE_RANK |
-----------------------------
| a     |    1 |          1 |
| a     |    1 |          1 |
| a     |    1 |          1 |
| b     |    4 |          2 |
| c     |    5 |          3 |
| c     |    5 |          3 |
| d     |    7 |          4 |
| e     |    8 |          5 |
-----------------------------
```

Example

The following query ranks the salaries of players, per team, whose salary is at least $1 million.

``` Example
SELECT DisplayName, Team, Season, Salary,
   RANK() OVER (PARTITION BY Team ORDER BY Salary Desc) "RANK"
   FROM Players JOIN Salaries  ON Salaries.ID=Players.ID 
   WHERE Salary>999999 AND Season=2015;

DISPLAYNAME             |TEAM     |SEASON|SALARY              |RANK 
---------------------------------------------------------------------
Mitch Hassleman         |Cards     |2015  |17000000            |1 
Yuri Milleton           |Cards     |2015  |15200000            |2 
James Grasser           |Cards     |2015  |9375000             |3 
Jack Hellman            |Cards     |2015  |8300000             |4 
Larry Lintos            |Cards     |2015  |7000000             |5 
Jeremy Johnson          |Cards     |2015  |4125000             |6 
Mitch Canepa            |Cards     |2015  |3750000             |7 
Mitch Brandon           |Cards     |2015  |3500000             |8 
Robert Cohen            |Cards     |2015  |3000000             |9 
James Woegren           |Cards     |2015  |2675000             |10
Sam Culligan            |Cards     |2015  |2652732             |11
Barry Morse             |Cards     |2015  |2379781             |12
Michael Rastono         |Cards     |2015  |2000000             |13
Carl Vanamos            |Cards     |2015  |2000000             |13
Alex Wister             |Cards     |2015  |1950000             |15
Pablo Bonjourno         |Cards     |2015  |1650000             |16
Jonathan Pearlman       |Cards     |2015  |1500000             |17
Jan Bromley             |Cards     |2015  |1200000             |18
Martin Cassman          |Giants    |2015  |20833333            |1 
Harry Pennello          |Giants    |2015  |18500000            |2 
Tam Lassiter            |Giants    |2015  |18000000            |3 
Buddy Painter           |Giants    |2015  |17277777            |4 
Thomas Hillman          |Giants    |2015  |12000000            |5 
Alex Paramour           |Giants    |2015  |10250000            |6 
Jack Peepers            |Giants    |2015  |9000000             |7 
Mark Briste             |Giants    |2015  |8000000             |8 
Marcus Bamburger        |Giants    |2015  |6950000             |9 
Jalen Ardson            |Giants    |2015  |6000000             |10
Steve Raster            |Giants    |2015  |6000000             |10
Sam Castleman           |Giants    |2015  |5000000             |12
Craig McGawn            |Giants    |2015  |4800000             |13
Norman Aikman           |Giants    |2015  |4000000             |14
Randy Varner            |Giants    |2015  |4000000             |14
Jason Lilliput          |Giants    |2015  |4000000             |14
Billy Bopper            |Giants    |2015  |3600000             |17
Greg Brown              |Giants    |2015  |3600000             |17
Mitch Lovell            |Giants    |2015  |3578825             |19
Bob Cranker             |Giants    |2015  |3175000             |20
Yuri Piamam             |Giants    |2015  |2100000             |21
Joseph Arkman           |Giants    |2015  |1450000             |22
Trevor Imhof            |Giants    |2015  |1100000             |23
Jason Minman            |Giants    |2015  |1000000             |24

42 rows selected
```

Here's the same query using <span class="CodeFont">DENSE\_RANK</span> instead of <span class="CodeFont">RANK</span>. Note how tied rankings are handled differently:

``` Example
SELECT DisplayName, Team, Season, Salary,
   DENSE_RANK() OVER (PARTITION BY Team ORDER BY Salary Desc) "RANK"
   FROM Players JOIN Salaries  ON Salaries.ID=Players.ID 
   WHERE Salary>999999 AND Season=2015;

DISPLAYNAME             |TEAM     |SEASON|SALARY              |RANK 
---------------------------------------------------------------------
Mitch Hassleman         |Cards     |2015  |17000000            |1 
Yuri Milleton           |Cards     |2015  |15200000            |2 
James Grasser           |Cards     |2015  |9375000             |3 
Jack Hellman            |Cards     |2015  |8300000             |4 
Larry Lintos            |Cards     |2015  |7000000             |5 
Jeremy Johnson          |Cards     |2015  |4125000             |6 
Mitch Canepa            |Cards     |2015  |3750000             |7 
Mitch Brandon           |Cards     |2015  |3500000             |8 
Robert Cohen            |Cards     |2015  |3000000             |9 
James Woegren           |Cards     |2015  |2675000             |10
Sam Culligan            |Cards     |2015  |2652732             |11
Barry Morse             |Cards     |2015  |2379781             |12
Michael Rastono         |Cards     |2015  |2000000             |13
Carl Vanamos            |Cards     |2015  |2000000             |13
Alex Wister             |Cards     |2015  |1950000             |14
Pablo Bonjourno         |Cards     |2015  |1650000             |15
Jonathan Pearlman       |Cards     |2015  |1500000             |16
Jan Bromley             |Cards     |2015  |1200000             |17
Martin Cassman          |Giants    |2015  |20833333            |1 
Harry Pennello          |Giants    |2015  |18500000            |2 
Tam Lassiter            |Giants    |2015  |18000000            |3 
Buddy Painter           |Giants    |2015  |17277777            |4 
Thomas Hillman          |Giants    |2015  |12000000            |5 
Alex Paramour           |Giants    |2015  |10250000            |6 
Jack Peepers            |Giants    |2015  |9000000             |7 
Mark Briste             |Giants    |2015  |8000000             |8 
Marcus Bamburger        |Giants    |2015  |6950000             |9 
Jalen Ardson            |Giants    |2015  |6000000             |10
Steve Raster            |Giants    |2015  |6000000             |10
Sam Castleman           |Giants    |2015  |5000000             |11
Craig McGawn            |Giants    |2015  |4800000             |12
Norman Aikman           |Giants    |2015  |4000000             |13
Randy Varner            |Giants    |2015  |4000000             |13
Jason Lilliput          |Giants    |2015  |4000000             |13
Billy Bopper            |Giants    |2015  |3600000             |14
Greg Brown              |Giants    |2015  |3600000             |14
Mitch Lovell            |Giants    |2015  |3578825             |15
Bob Cranker             |Giants    |2015  |3175000             |16
Yuri Piamam             |Giants    |2015  |2100000             |17
Joseph Arkman           |Giants    |2015  |1450000             |18
Trevor Imhof            |Giants    |2015  |1100000             |19
Jason Minman            |Giants    |2015  |1000000             |20

42 rows selected
```

See Also

-   [Window and Aggregate](Intro.WindowAggregrateFcns.html)functions
-   [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html) data type
-   [<span class="CodeFont">DENSE\_RANK</span>](DenseRank.html) function
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause
-   <span class="ItalicFont">[Working with Dates](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span>

 


