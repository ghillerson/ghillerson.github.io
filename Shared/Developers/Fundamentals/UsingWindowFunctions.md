[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/UsingWindowFunctions.html)

Splice Machine Window Functions
===============================

An SQL <span class="ItalicFont">window function</span> performs a calculation across a set of table rows that are related to the current row, either by proximity in the table, or by the value of a specific column or set of columns; these columns are known as the <span class="ItalicFont">partition</span>.

This topic provides a very quick summary of window functions, as implemented in Splice Machine. For more general information about SQL window functions, we recommending visiting some of the sources listed in the <a href="#ForMoreInfo" class="selected">Additional Information</a> section at the end of this topic.

Here's a quick example of using a window function to operate on the following table:

| OrderID | CustomerID | Amount |
|---------|------------|--------|
| 123     | 1          | 100    |
| 144     | 1          | 250    |
| 167     | 1          | 150    |
| 202     | 1          | 250    |
| 209     | 1          | 325    |
| 224     | 1          | 125    |
| 66      | 2          | 100    |
| 94      | 2          | 200    |
| 127     | 2          | 300    |
| 444     | 2          | 400    |

This query will find the first Order ID for each specified Customer ID in the above table:

``` Example
SELECT OrderID, CustomerID,
    FIRST_VALUE(OrderID) OVER (
        PARTITION BY CustomerID
        ORDER BY OrderID
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW )
AS FirstOrderID
FROM ORDERS
WHERE CustomerID IN (1,2);
```

This works by partitioning (grouping) the selected rows by CustomerID, ordering them for purposes of applying the function to the rows in the partition, and then using the <span class="CodeFont">FIRST\_VALUE</span> window function to evaluate the OrderID values in each partition and find the first value in each. The results for our sample table are:

| OrderID | CustomerID | FirstOrderID |
|---------|------------|--------------|
| 123     | 1          | 123          |
| 144     | 1          | 123          |
| 167     | 1          | 123          |
| 202     | 1          | 123          |
| 209     | 1          | 123          |
| 224     | 1          | 123          |
| 66      | 2          | 66           |
| 94      | 2          | 66           |
| 127     | 2          | 66           |
| 444     | 2          | 66           |

See the <a href="#Window2" class="selected">Window Frames</a> section below for a further explanation of this query.

About Window Functions
----------------------

Window functions:

-   Operate on a window, or set of rows. The rows considered by a window function are produced by the query's <span class="CodeFont">FROM</span> clause as filtered by its <span class="CodeFont">WHERE</span>, <span class="CodeFont">GROUP BY</span>, and <span class="CodeFont">HAVING</span> clauses, if any. This means that any row that doesn't meet the <span class="CodeFont">WHERE</span> condition is not seen by a window function.
-   Are similar to aggregate functions, except that a window function does not group rows into a single output row. Instead, a window function returns a value for every row in the window. This is sometimes referred to as tuple-based aggregation.
-   The values are calculated from the set of rows in the window.
-   Always contain an <span class="CodeFont">OVER</span> clause, which determines how the rows of the query are divided and sequenced for processing by the window function.
-   The <span class="CodeFont">OVER</span> clause can contain a <span class="CodeFont">PARTITION</span> clause that specifies the set of rows in the table that form the window, relative to the current row.
-   The <span class="CodeFont">OVER</span> clause can contain an optional <span class="CodeFont">ORDER BY</span> clause that specifies in which order rows are processed by the window function. This <span class="CodeFont">ORDER BY</span> clause is independent of the <span class="CodeFont">ORDER BY</span> clause that specifies the order in which rows are output.

    Note that the <a href="#The3" class="selected">ranking functions</a> (<span class="CodeFont">[DENSE\_RANK](../../SQLReference/BuiltInFcns/DenseRank.html)</span>, <span class="CodeFont">[RANK](../../SQLReference/BuiltInFcns/Rank.html)</span>, and <span class="CodeFont">[ROW NUMBER](../../SQLReference/BuiltInFcns/RowNumber.html))</span> <span class="BoldFont">must contain</span> an <span class="CodeFont">ORDER BY</span> clause.

-   The <span class="CodeFont">OVER</span> clause can also contain an optional <span class="ItalicFont">frame clause</span> that further restricts which of the rows in the partition are sent to the function for evaluation.

### About Windows, Partitions, and Frames

Using window functions can seem complicated because they involve a number of overlapping terms, including <span class="ItalicFont">window</span>, <span class="ItalicFont">sliding window</span>, <span class="ItalicFont">partition</span>, <span class="ItalicFont">set</span>, and <span class="ItalicFont">window frame</span>. An additional complication is that window frames can be specified using either <span class="ItalicFont">rows</span> or <span class="ItalicFont">ranges</span>.

Let's start with basic terminology definitions:

| Terms               | Description                                                                                                                                                                                                                                                                                    |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| window function     | A function that operates on a set of rows and produces output for each row.                                                                                                                                                                                                                    |
| window partition    | The grouping of rows within a table.                                                                                                                                                                                                                                                           
                                                                                                                                                                                                                                                                                                                       
                       Note that window partitions retains the rows, unlike aggregates,                                                                                                                                                                                                                                |
| window ordering     | The sequence of rows within each partition; this is the order in which the rows are passed to the window function for evaluation.                                                                                                                                                              |
| window frame        | A frame of rows within a window partition, relative to the current row. The window frame is used to further restrict the set of rows operated on by a function, and is sometimes referred to as the <span class="ItalicFont">row or range</span> clause.                                       |
| OVER clause         | This is the clause used to define how the rows of the table are divided, or partitioned, for processing by the window function. It also orders the rows within the partition.                                                                                                                  
                                                                                                                                                                                                                                                                                                                       
                       See the <a href="#The" class="selected">The OVER Clause</a> section below for more information.                                                                                                                                                                                                 |
| partitioning clause | An optional part of an <span class="CodeFont">OVER</span> clause that divides the rows into partitions, similar to using the <span class="CodeFont">GROUP BY</span> clause. The default partition is all rows in the table, though window functions are generally calculated over a partition. 
                                                                                                                                                                                                                                                                                                                       
                       See the <a href="#Window" class="selected">The Partition Clause</a> section below for more information.                                                                                                                                                                                         |
| ordering clause     | Defines the ordering of rows within each partition.                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                                                                                                       
                       See the <a href="#The2" class="selected">The Order Clause</a> section below for more information.                                                                                                                                                                                               |
| frame clause        | Further refines the set of rows when you include an <span class="CodeFont">ORDER BY</span> clause in your window function specification, by allowing you to include or exclude rows or values within the ordering.                                                                             
                                                                                                                                                                                                                                                                                                                       
                       See the <a href="#Window2" class="selected">The Frame Clause</a> section below for examples and more information.                                                                                                                                                                               |

### []()The OVER Clause

A window function alway contains an <span class="CodeFont">OVER</span> clause, which determines how the rows of the query are divided, or partitioned, for processing by the window function.

``` FcnSyntax
expression OVER( 
     [partitionClause]
     [orderClause]
     [frameClause] );
 
```

expression

Any value expression that does not itself contain window function calls.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>When you use an [aggregate function](../../SQLReference/BuiltInFcns/Intro.WindowAggregrateFcns.html) such as <span class="CodeFont">AVG</span> with an <span class="CodeFont">OVER</span> clause, the aggregated value is computed per partition.

### []()The Partition Clause

The partition clause, which is optional, specifies how the window function is broken down over groups, in the same way that <span class="CodeFont">GROUP BY</span> specifies groupings for regular aggregate functions. Some example partitions are:

-   departments within an organization
-   regions within a geographic area
-   quarters within years for sales

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you omit the partition clause, the default partition, which contains all rows in the table, is used.However, since window functions are used to perform calculations over subsets (partitions) of rows in a table, you generally should specify a partition clause.

Syntax

``` FcnSyntax
PARTITION BY expression [, ...]
```

expression \[,...\]

A list of expressions that define the partitioning.

If you omit this clause, there is one partition that contains all rows in the entire table.

Here's a simple example of using the partition clause to compute the average order amount per customer:

``` Example
SELECT OrderID, CustomerID, Amount,
    Avg(Amount) OVER (
        PARTITION BY CustomerID
        ORDER BY OrderID
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW )
AS AverageOrderAmt FROM ORDERS
WHERE CustomerID IN (1,2);
```

| OrderID | CustomerID | Amount | AverageOrderAmt |
|---------|------------|--------|-----------------|
| 123     | 1          | 100    | 200             |
| 144     | 1          | 250    | 200             |
| 167     | 1          | 150    | 200             |
| 202     | 1          | 250    | 200             |
| 209     | 1          | 325    | 200             |
| 224     | 1          | 125    | 200             |
| 66      | 2          | 100    | 250             |
| 94      | 2          | 200    | 250             |
| 127     | 2          | 300    | 250             |
| 444     | 2          | 400    | 250             |

### []()The Order Clause

You can also control the order in which rows are processed by window functions using <span class="CodeFont">ORDER BY</span> within your <span class="CodeFont">OVER</span> clause. This is optional, though it is important for any ranking or cumulative functions.

Syntax

``` FcnSyntax
ORDER BY expression 
   [ ASC | DESC | USING operator ]
   [ NULLS FIRST | NULLS LAST ]
   [, ...]
```

Some notes about the <span class="CodeFont">ORDER BY</span> clause in an <span class="CodeFont">OVER</span> clause:

-   Ascending order (<span class="CodeFont">ASC</span>) is the default ordering.
-   If you specify <span class="CodeFont">NULLS LAST</span>, then <span class="CodeFont">NULL</span> values are returned last; this is the default when you use <span class="CodeFont">ASC</span> order.
-   If you specify <span class="CodeFont">NULLS FIRST</span>, then <span class="CodeFont">NULL</span> values are returned first; this is the default when you use <span class="CodeFont">DESC</span> order.
-   The <span class="CodeFont">ORDER BY</span> clause in your <span class="CodeFont">OVER</span> clause <span class="ItalicFont">does not</span> have to match the order in which the rows are output.
-   You can only specify a <span class="ItalicFont">frame clause</span> if you include an <span class="CodeFont">ORDER BY</span> clause in your <span class="CodeFont">OVER</span> clause.

### []()The Frame Clause

The optional frame clause defines which of the rows in the partition (the <span class="CodeFont">frame</span>) should be evaluated by the window function. You can limit which rows in the partition are passed to the function in two ways:

-   Specify a <span class="CodeFont">ROWS</span> frame to limit the frame to a fixed number of rows from the partition that precede or follow the current row.
-   Specify <span class="CodeFont">RANGE</span> to only include rows in the frame whose evaluated value falls within a certain range of the current row's value. This is the default, and the current default range is <span class="CodeFont">1</span>, which means that only rows whose value matches that of the current row are passed to the function.

Some sources refer to the frame clause as the <span class="ItalicFont">Rows or Ranges</span> clause. If you omit this clause, the default is to include all rows

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Window frames can only be used when you include an <span class="CodeFont">ORDER BY</span> clause within the <span class="CodeFont">OVER</span> clause.

Syntax

This clause specifies two offsets: one determines the start of the window frame, and the other determines the end of the window frame.

``` FcnSyntax
[RANGE | ROWS] frameStart |
[RANGE | ROWS] BETWEEN frameStart AND frameEnd
```

<span class="CodeFont">RANGE</span>

The frame includes rows whose values are within a specified range of the current row's value.

The range is determined by the <span class="CodeFont">ORDER BY</span> column(s). Rows with identical values for their <span class="CodeFont">ORDER BY</span> columns are referred to as <span class="ItalicFont">peer rows</span>.

<span class="CodeFont">ROWS</span>

The frame includes a fixed number of rows based on their position in the table relative to the current row.

frameStart

Specifies the start of the frame.

For <span class="CodeFont">ROWS</span> mode, you can specify:

> ``` FcnSyntax
> UNBOUNDED PRECEDING 
> | value PRECEDING
> | CURRENT ROW
> | value FOLLOWING
> ```
>
> <span class="CodeItalicFont">value</span>
>
> A non-negative integer value.
>
For <span class="CodeFont">RANGE</span> mode, you can only specify:

> ``` FcnSyntax
> CURRENT ROW
> | UNBOUNDED FOLLOWING
> ```
>
frameEnd

Specifies the end of the frame. The default value is <span class="CodeFont">CURRENT ROW</span>.

For <span class="CodeFont">ROWS</span> mode, you can specify:

> ``` FcnSyntax
> value PRECEDING
> | CURRENT ROW
> | value FOLLOWING
> | UNBOUNDED FOLLOWING
> ```
>
> <span class="CodeItalicFont">value</span>
>
> A non-negative integer value.
>
For <span class="CodeFont">RANGE</span> mode, you can only specify:

> ``` FcnSyntax
> CURRENT ROW
> | UNBOUNDED FOLLOWING
> ```
>
Ranges and Rows

Probably the easiest way to understand how <span class="CodeFont">RANGE</span> and <span class="CodeFont">ROWS</span> work is by way of some simple <span class="CodeFont">OVER</span> clause examples:

> ##### []()Example 1:
>
> This clause can be used to apply a window function to all rows in the partition from the top of the partition to the current row:
>
> ``` Example
> OVER (PARTITION BY customerID ORDER BY orderDate)
> ```
>
> ##### Example 2:
>
> Both of these clauses specify the same set of rows as <a href="#Example" class="selected">Example 1:</a>
>
> ``` Example
> OVER (PARTITION BY customerID ORDER BY orderDate UNBOUNDED PRECEDING preceding)
>
> OVER (PARTITION BY customerID ORDER BY orderDate RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
> ```
>
> ##### Example 3:
>
> This clause can be used to apply a window function to the current row and the 3 preceding row's values in the partition:
>
> ``` Example
> OVER (PARTITION BY customerID ORDER BY orderDate ROWS 3 preceding)
> ```

FrameStart and FrameEnd

Some important notes about the frame clause:

-   <span class="CodeFont">UNBOUNDED PRECEDING</span> means that the frame starts with the first row of the partition.
-   <span class="CodeFont">UNBOUNDED FOLLOWING</span> means that the frame ends with the last row of the partition.
-   You must specify the <span class="CodeItalicFont">frameStart</span> first and the <span class="CodeItalicFont">frameEnd</span> last within the frame clause.
-   In <span class="CodeFont">ROWS</span> mode, <span class="CodeFont">CURRENT ROW</span> means that the frame starts or ends with the current row; in <span class="CodeFont">RANGE</span> mode, <span class="CodeFont">CURRENT ROW</span> means that the frame starts or ends with the current row's first or last peer in the <span class="CodeFont">ORDER BY</span> ordering.
-   The default <span class="ItalicFont">frameClause</span> is to include all values from the start of the partition through the current row: 

    ``` Example
    RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ```

Common Frame Clauses

When learning about window functions, you may find references to these specific frame clause types:

| Frame Clause Type | Example                                             |
|-------------------|-----------------------------------------------------|
| Recycled          | BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING |
| Cumulative        | BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW         |
| Rolling           | BETWEEN 2 PRECEDING AND 2 FOLLOWING                 |

### Examples

This is a simple example that doesn't use a frame clause:

1.  Rank each year within a player by the number of home runs hit by that player:

    ``` Example
    RANK() OVER (PARTITION BY playerID ORDER BY H desc); 
    ```

Here are some examples of window functions using frame clauses:

1.  Compute the running sum of G for each player:

    ``` Example
    SUM(G) OVER (PARTITION BY playerID ORDER BY yearID
      RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW); 
    ```

2.  Compute the career year:

    ``` Example
    YearID - min(YEARID) OVER (PARTITION BY playerID
       RANGE BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) + 1; 
    ```

3.  Compute a rolling average of games by player:

    ``` Example
    AVG(G) OVER (PARTITION BY playerID ORDER BY yearID
       ROWS BETWEEN 2 PRECEDING AND 2 FOLLOWING); 
    ```

[]()The Ranking Functions
-------------------------

A subset of our window functions are known as <span class="ItalicFont">ranking functions</span>:

-   [DENSE\_RANK](../../SQLReference/BuiltInFcns/DenseRank.html)<span class="bodyFont"> ranks each row in the result set. If values in the ranking column are the same, they receive the same rank. The next number in the ranking sequence is then used to rank the row or rows that follow, which means that <span class="CodeFont">DENSE\_RANK</span> always returns consecutive numbers.</span>
-   [RANK](../../SQLReference/BuiltInFcns/Rank.html)<span class="bodyFont"> ranks each row in the result set. If values in the ranking column are the same, they receive the same rank. However, the next number in the ranking sequence is then skipped, which means that <span class="CodeFont">RANK</span> can return non-consecutive numbers.</span>
-   [ROW NUMBER](../../SQLReference/BuiltInFcns/RowNumber.html)<span class="bodyFont"> assigns a sequential number to each row in the result set.</span>

All ranking functions <span class="BoldFont">must include</span> an <span class="CodeFont">ORDER BY</span> clause in the <span class="CodeFont">OVER()</span> clause, since that is how they compute ranking values.

Window Function Restrictions
----------------------------

Because window functions are only allowed in <span class="CodeFont">[SELECT](../../SQLReference/Statements/Select.html)</span> and <span class="CodeFont">[ORDER BY](../../SQLReference/Clauses/OrderBy.html)</span> clauses, and because window functions are computed after both <span class="CodeFont">WHERE</span> and <span class="CodeFont">HAVING</span>, you sometimes need to use subqueries with window functions to accomplish what seems like it could be done in a simpler query.

For example, because you cannot use an <span class="CodeFont">OVER</span> clause in a <span class="CodeFont">WHERE</span> clause, a query like the following is not possible:

``` Example
SELECT *
FROM Batting
WHERE rank() OVER (PARTITION BY playerID ORDER BY G) = 1;
```

And because <span class="CodeFont">WHERE</span> and <span class="CodeFont">HAVING</span> are computed before the windowing functions, this won't work either:

``` Example
SELECT playerID, rank() OVER (PARTITION BY playerID ORDER BY G) as player_rank FROM Batting
WHERE player_rank = 1;
```

Instead, you need to use a subquery:

``` Example
SELECT *
FROM (
   SELECT playerID, G, rank() OVER (PARTITION BY playerID ORDER BY G) as "pos"
   FROM Batting
) tmp
WHERE "pos" = 1;
```

And note that the above subquery will add a rank column to the original columns,

[]()Window Functions Included in This Release
---------------------------------------------

Splice Machine is currently expanding the set of SQL functions already able to take advantage of windowing functionality.

The <span class="CodeFont">[OVER](../../SQLReference/Clauses/Over.html)</span> clause topic in our <span class="ItalicFont">SQL Reference</span> completes the complete reference information for <span class="CodeFont">OVER</span>.

Here is a list of the functions that currently support windowing:

-   [AVG](../../SQLReference/BuiltInFcns/Avg.html)
-   [COUNT](../../SQLReference/BuiltInFcns/Count.html)
-   [DENSE\_RANK](../../SQLReference/BuiltInFcns/DenseRank.html)
-   [FIRST\_VALUE](../../SQLReference/BuiltInFcns/FirstValue.html)
-   [LAG](../../SQLReference/BuiltInFcns/Lag.html)
-   [LAST\_VALUE](../../SQLReference/BuiltInFcns/LastValue.html)
-   [LEAD](../../SQLReference/BuiltInFcns/Lead.html)
-   [MAX](../../SQLReference/BuiltInFcns/Max.html)
-   [MIN](../../SQLReference/BuiltInFcns/Min.html)
-   [RANK](../../SQLReference/BuiltInFcns/Rank.html)
-   [ROW NUMBER](../../SQLReference/BuiltInFcns/RowNumber.html)
-   [SUM](../../SQLReference/BuiltInFcns/Sum.html)

[]()Additional Information
--------------------------

There are numerous articles about window functions that you can find online. Here are a few you might find valuable:

-   The [simple talk articles from Red Gate](https://www.simple-talk.com/sql/learn-sql-server/window-functions-in-sql-server/) about window functions are probably the most straightforward and comprehensive descriptions of window functions.
-   This [Oracle Technology Network article](http://www.oracle.com/technetwork/issue-archive/2013/13-mar/o23sql-1906475.html) provides an excellent technical introduction.
-   This [PostgreSQL page](http://www.postgresql.org/docs/9.1/static/tutorial-window.html) introduces their version of window functions and links to other pages.
-   This [PostgreSQL wiki page](https://wiki.postgresql.org/wiki/SQL2008_windowing_queries) about SQL windowing queries page provides a succinct explanation of why windowing functions are used, and includes several useful examples.
-   The [Wikipedia SQL SELECT](http://en.wikipedia.org/wiki/Select_(SQL)) page contains descriptions of specific window functions and links to other pages.

 


