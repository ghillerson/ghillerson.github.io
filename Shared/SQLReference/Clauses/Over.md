[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Over.html)

[]()OVER
========

The <span class="CodeFont">OVER</span> clause is used in window functions to define the window on which the function operates. Window functions are permitted only in the <span class="CodeFont">[SELECT](../Statements/Select.html)</span> list and the <span class="CodeFont">[ORDER BY](OrderBy.html)</span> clause of queries.

For general information about and examples of Window functions in Splice Machine, see the [Using Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html) topic in our <span class="ItalicFont">Splice Machine Developer's Guide</span>.

Syntax

``` FcnSyntax
expression OVER( 
     [partitionClause]
     [orderClause]
     [frameClause] );
```

expression

Any value expression that does not itself contain window function calls.

partitionClause

Optional. Specifies how the window function is broken down over groups, in the same way that <span class="CodeFont">GROUP BY</span> specifies groupings for regular aggregate functions. If you omit this clause, there is one partition that contains all rows.

The syntax for this clause is essentially the same as for the <span class="CodeFont">[GROUP BY](GroupBy.html)</span> clause for queries; To recap:

``` FcnSyntax
PARTITION BY expression [, ...]
```

expression \[,...\]

A list of expressions that define the partitioning.

orderClause

Optional. Controls the ordering. It is important for ranking functions, since it specifies by which variables ranking is performed. It is also needed for cumulative functions. The syntax for this clause is essentially the same as for the <span class="CodeFont">[ORDER BY](OrderBy.html)</span> clause for queries, as described in our [SQL Reference](OrderBy.html). To recap:

``` FcnSyntax
ORDER BY expression 
   [ ASC | DESC | USING operator ]
   [ NULLS FIRST | NULLS LAST ]
   [, ...]
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The default ordering is ascending (<span class="CodeFont">ASC</span>). For ascending order, <span class="CodeFont">NULL</span> values are returned last unless you specify <span class="CodeFont">NULLS FIRST</span>; for descending order, <span class="CodeFont">NULL</span> values are returned first unless you specify <span class="CodeFont">NULLS LAST</span>.

frameClause

Optional. Defines which of the rows (which <span class="ItalicFont">frame</span>) that are passed to the window function should be included in the computation. The <span class="ItalicFont">frameClause</span> provides two offsets that determine the start and end of the frame.

The syntax for the frame clause is:

``` FcnSyntax
[RANGE | ROWS] frameStart |
[RANGE | ROWS] BETWEEN frameStart AND frameEnd
```

The syntax for both <span class="ItalicFont">frameStart</span> and <span class="ItalicFont">frameEnd</span> is:

``` FcnSyntax
UNBOUNDED PRECEDING |
<n> PRECEDING       |
CURRENT ROW         |
<n> FOLLOWING       |
UNBOUNDED FOLLOWING 
```

&lt;n&gt;

A a non-negative integer value.

Usage Restrictions

Because window functions are only allowed in <span class="CodeFont">[SELECT](../Statements/Select.html)</span> and <span class="CodeFont">[ORDER BY](OrderBy.html)</span> clauses, and because window functions are computed after both the <span class="CodeFont">[WHERE](Where.html)</span> and <span class="CodeFont">[HAVING](Using.html)</span>clauses, you sometimes need to use subqueries with window functions to accomplish what seems like it could be done in a simpler query.

For example, because you cannot use an <span class="CodeFont">OVER</span> clause in a <span class="CodeFont">WHERE</span> clause, a query like the following is not possible:

``` Example
SELECT *
FROM Batting
WHERE rank() OVER (PARTITION BY "playerID" ORDER BY "G") = 1;
```

And because <span class="CodeFont">WHERE</span> and <span class="CodeFont">HAVING</span> are computed before the windowing functions, this won't work either:

``` Example
SELECT *, rank() OVER (PARTITION BY "playerID" ORDER BY "G") as rank
FROM Batting
WHERE rank = 1;
```

Instead, you need to use a subquery:

``` Example
SELECT *
FROM (
   SELECT *, rank() OVER (PARTITION BY "playerID" ORDER BY "G") as rank
   FROM Batting
) tmp
WHERE rank = 1;
```

And note that the above subquery will add a rank column to the original columns,

Simple Window Function Examples

The examples in this section are fairly simple because they don't use the frame clause.

``` Example
--- Rank each year within a player by the number of home runs hit by that player
RANK() OVER (PARTITION BY playerID ORDER BY desc(H)); 

--- Compute the change in number of games played from one year to the next:
G - LAG(G) OVER (PARTITION G playerID ORDER BY yearID); 
```

Examples with Frame Clauses

The frame clause can be confusing, given all of the options that it presents. There are three commonly used frame clauses:

| Frame Clause Type | Example                                              |
|-------------------|------------------------------------------------------|
| Recycled          | BETWEEN UNBOUNDED PRECEEDING AND UNBOUNDED FOLLOWING |
| Cumulative        | BETWEEN UNBOUNDED PRECEEDING AND CURRENT ROW         |
| Rolling           | BETWEEN 2 PRECEEDING AND 2 FOLLOWING                 |

Here are some examples of window functions using frame clauses:

``` Example
--- Compute the running sum of G for each player:
SUM(G) OVER (PARTITION BY playerID ORDER BY yearID
  BETWEEN UNBOUNDED PRECEEDING AND CURRENT ROW); 

--- Compute the career year:
YearID - min(YEARID) OVER (PARTITION BY playerID
   BETWEEN UNBOUNDED PRECEEDING AND UNBOUNDED FOLLOWING) + 1;

--- Compute a rolling average of games by player:
MEAN(G) OVER (PARTITION BY playerID ORDER BY yearID
   BETWEEN 2 PRECEEDING AND 2 FOLLOWING); 
```

See Also

-   [Window and Aggregate](../BuiltInFcns/Intro.WindowAggregrateFcns.html)functions
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">HAVING</span>](Having.html) clause
-   [<span class="CodeFont">ORDER BY</span>](OrderBy.html) clause
-   [<span class="CodeFont">WHERE</span>](Where.html) clause
-   The [Using Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html) section in our <span class="ItalicFont">Splice Machine Developer's Guide</span>

 


