[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/RowNumber.html)

<a href="" id="BuiltInFcns.RowNumber"></a>[]()ROW\_NUMBER
=========================================================

<span class="CodeFont">ROW\_NUMBER()</span> is a <span class="ItalicFont">ranking function</span> that numbers the rows within the ordered partition of values defined by its <span class="CodeFont">OVER</span> clause. Ranking functions are a subset of [window functions](Intro.WindowAggregrateFcns.html).

Syntax

``` FcnSyntax
ROW_NUMBER() OVER ( overClause )
```

overClause

See the <span class="CodeFont">[OVER](../Clauses/Over.html)</span> clause documentation.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Ranking functions such as <span class="CodeFont">ROW\_NUMBER</span> must include an <span class="CodeFont">[ORDER BY](../Clauses/OrderBy.html)</span> clause in the <span class="CodeFont">OVER</span> clause. This is because the ranking is calculated based on the ordering.

Results

The resulting data type is <span class="CodeFont">[BIGINT](../DataTypes/BigInt.html)</span>.

Example

The following query ranks the salaries of players on the Cards whose salaries are at least $1 million:

``` Example
splice> SELECT DisplayName, Salary, 
   ROW_NUMBER() OVER (PARTITION BY Team ORDER BY Salary DESC) "RowNum" 
   FROM Players JOIN Salaries ON Players.ID=Salaries.ID 
   WHERE Team='Cards' and Salary>999999;

DISPLAYNAME             |SALARY              |RowNum              
------------------------------------------------------------------
Mitch Hassleman         |17000000            |1                   
Yuri Milleton           |15200000            |2                   
James Grasser           |9375000             |3                   
Jack Hellman            |8300000             |4                   
Larry Lintos            |7000000             |5                   
Jeremy Johnson          |4125000             |6                   
Mitch Canepa            |3750000             |7                   
Mitch Brandon           |3500000             |8                   
Robert Cohen            |3000000             |9                   
James Woegren           |2675000             |10                  
Sam Culligan            |2652732             |11                  
Barry Morse             |2379781             |12                  
Michael Rastono         |2000000             |13                  
Carl Vanamos            |2000000             |14                  
Alex Wister             |1950000             |15                  
Pablo Bonjourno         |1650000             |16                  
Jonathan Pearlman       |1500000             |17                  
Jan Bromley             |1200000             |18                  

18 rows selected
```

See Also

-   [Window and Aggregate](Intro.WindowAggregrateFcns.html)functions
-   [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html) data type
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause
-   [<span class="CodeFont">OVER</span>](../Clauses/Over.html) clause
-   <span class="ItalicFont">[Using Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html)</span> in the <span class="ItalicFont">Developer Guide</span>.

 


