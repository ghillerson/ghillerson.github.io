[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInFcns/Intro.WindowAggregrateFcns.html)

[]()Window and Aggregate Functions
==================================

This section contains the Aggregate and Window (analytic) functions built into Splice Machine SQL.

-   [Aggregate functions](#Aggregat), which are sometimes referred to as set functions, provide a means of evaluating an expression over a set of rows. Each aggregate function outputs one value for the set of rows on which it operates. All aggregate functions can also be used as window functions.
-   [Window functions](#Window), which are sometimes referred to as <span class="ItalicFont">analytic functions</span>, perform calculations across a set of table rows that are related to the current row. Each window function outputs one value for each row on which it operates. Some of the window functions <span class="ItalicFont">cannot</span> be used as aggregate functions.

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>A subset of the window functions are sometimes referred to as <span class="ItalicFont">ranking functions</span>, as noted below.

| <span class="BoldFont">Function Name</span>                   | Window or Aggregate | Description                                                                                                                                              | Permitted Data Types                                              |
|---------------------------------------------------------------|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| <span class="CodeFont">[AVG](Avg.html)</span>                 | Both                | Returns the average computed over a subset (partition) of a table.                                                                                       | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[COUNT](Count.html)</span>             | Both                | Returns the number of rows in a partition.                                                                                                               | All types.                                                        |
| <span class="CodeFont">[DENSE\_RANK](DenseRank.html)</span>   | Window              | A ranking function that returns the ranking of a row within a partition.                                                                                 | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[FIRST\_VALUE](FirstValue.html)</span> | Window              | Returns the first value within a partition..                                                                                                             | All types.                                                        |
| <span class="CodeFont">[LAG](Lag.html)</span>                 | Window              | Returns the value of an expression evaluated at a specified offset number of rows <span class="ItalicFont">before</span> the current row in a partition. | All types.                                                        |
| <span class="CodeFont">[LAST\_VALUE](LastValue.html)</span>   | Window              | Returns the last value within a partition..                                                                                                              | All types.                                                        |
| <span class="CodeFont">[LEAD](Lead.html)</span>               | Window              | Returns the value of an expression evaluated at a specified offset number of rows <span class="ItalicFont">after</span> the current row in a partition.  | All types.                                                        |
| <span class="CodeFont">[MAX](Max.html)</span>                 | Both                | Returns the maximum value computed over a partition.                                                                                                     | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[MIN](Min.html)</span>                 | Both                | Returns the minimum value computed over a partition.                                                                                                     | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[RANK](Rank.html)</span>               | Window              | A ranking function that returns the ranking of a row within a subset of a table.                                                                         | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[ROW\_NUMBER](RowNumber.html)</span>   | Window              | A ranking function that returns the row number of a row within a partition.                                                                              | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[STDDEV\_POP](StdDevPop.html)</span>   | Both                | Returns the sum of a value calculated over a partition.                                                                                                  | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[STDDEV\_SAMP](StdDevSamp.html)</span> | Both                | Returns the sum of a value calculated over a partition.                                                                                                  | The [numeric built-in data types](#numeric_built-in_data_types_). |
| <span class="CodeFont">[SUM](Sum.html)</span>                 | Both                | Returns the sum of a value calculated over a partition.                                                                                                  | The [numeric built-in data types](#numeric_built-in_data_types_). |

### []()The Numeric Built-in Data Types

The numeric built-in data types are: [<span class="CodeFont">DECIMAL</span>](../DataTypes/Decimal.html), [<span class="CodeFont">DOUBLE PRECISION</span>](../DataTypes/DoublePrecision.html), [<span class="CodeFont">FLOAT</span>](../DataTypes/Float.html), [<span class="CodeFont">INTEGER</span>](../DataTypes/Integer.html), [<span class="CodeFont">BIGINT</span>](../DataTypes/BigInt.html), [<span class="CodeFont">NUMERIC</span>](../DataTypes/Numeric.html), [<span class="CodeFont">REAL</span>](../DataTypes/Real.html), and [<span class="CodeFont">SMALLINT</span>](../DataTypes/SmallInt.html).

[]()Using Aggregate Functions
-----------------------------

Aggregate functions (also described as <span class="ItalicFont">set functions</span> in ANSI SQL and as <span class="ItalicFont">column functions</span> in some database literature). They provide a means of evaluating an expression over a set of rows.

Whereas the other built-in functions operate on a single expression, aggregates operate on a set of values and reduce them to a single scalar value. Built-in aggregates can calculate the minimum, maximum, sum, count, and average of an expression over a set of values as well as count rows. The following table shows the data types on which each built-in aggregate function can operate.

Aggregates are permitted only in the following:

-   A <span class="ItalicFont">SelectItem</span> in a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html).</span>
-   A [<span class="CodeFont">HAVING</span> clause](../Clauses/Having.html).
-   An [<span class="CodeFont">ORDER BY</span> clause](../Clauses/OrderBy.html) (using an alias name) if the aggregate appears in the result of the relevant query block. That is, an alias for an aggregate is permitted in an [<span class="CodeFont">ORDER BY</span> clause](../Clauses/OrderBy.html) if and only if the aggregate appears in a <span class="ItalicFont">SelectItem</span> in a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html).</span>

All expressions in <span class="ItalicFont">SelectItems</span> in the <span class="ItalicFont">[SelectExpression](../Expressions/Select.html)</span> must be either aggregates or grouped columns (see [<span class="CodeFont">GROUP BY</span> clause](../Clauses/GroupBy.html)).(The same is true if there is a <span class="CodeFont">HAVING</span> clause without a <span class="CodeFont">GROUP BY</span> clause.)

This is because the <span class="ItalicFont">ResultSet</span> of a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html)</span> must be either a scalar (single value) or a vector (multiple values), but not a mixture of both. (Aggregates evaluate to a scalar value, and the referenceto a column can evaluate to a vector.) For example, the following query mixes scalar and vector values and thus is not valid:

``` Example
   -- not valid
SELECT MIN(flying_time), flight_id
  FROM Flights;
```

Aggregates are not allowed on outer references (correlations). This means that if a subquery contains an aggregate, that aggregate cannot evaluate an expression that includes a reference to a column in the outer query block. For example, the following query is not valid because SUM operates on a column from the outer query:

``` Example
SELECT c1
  FROM t1
  GROUP BY c1
  HAVING c2 >
  SELECT t2.x
  FROM t2
  WHERE t2.y = SUM(t1.c3));
```

[]()Using Window Functions
--------------------------

Window functions, sometimes referred to as <span class="ItalicFont">analytic</span> functions, perform calculations across a set of table rows that are related to the current row. They are similar to aggregate functions, with several significant differences; a window function:

-   Always includes an <span class="CodeFont">[OVER](../Clauses/Over.html)</span> clause
-   Outputs one row for each input value it operates upon.
-   Groups rows with window partitioning and frame clauses, rather than using <span class="CodeFont">[GROUP BY](../Clauses/GroupBy.html)</span> clauses

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Most developers who are new to window functions find that the easiest way to understand them is to view examples, such as the ones in the [Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html) topic in our <span class="ItalicFont">Splice Machine Developer's Guide</span>.

Window functions can be used to handle complex analysis and reporting. For example, it's easy to output running totals, moving averages for a specific time frame, and similar functions. There are a few simple rules about window function usage you need to know:

-   Window functions are permitted only in the <span class="CodeFont">SELECT</span> list and the <span class="CodeFont">ORDER BY</span> clause of the query. They are forbidden elsewhere, such as in <span class="CodeFont">GROUP BY</span>, <span class="CodeFont">HAVING</span> and <span class="CodeFont">WHERE</span> clauses. These restrictions are due to the fact that window functions execute after the processing of those clauses.
-   You can include an aggregate function call in the arguments to a window function; however, you cannot include a window function in the arguments to a regular aggregate function. This is again due to the fact that window functions execute after regular aggregate functions have executed.
-   When the function runs, a window of rows is computed in relation to the current row; as the current row advances, the window moves along with it.

The rows considered by a window function (its input rows) are those of the <span class="ItalicFont">virtual table</span> produced by the query's <span class="CodeFont">FROM</span> clause as filtered by its <span class="CodeFont">WHERE</span>, <span class="CodeFont">GROUP BY</span>, and <span class="CodeFont">HAVING</span> clauses, if any. This means, for example, that a row removed because it does not meet the <span class="CodeFont">WHERE</span> condition is not seen by any window function. A query can contain multiple window functions that slice up the data in different ways by means of different <span class="CodeFont">OVER</span> clauses, but they all act on the same collection of rows defined by this virtual table.

For examples and further explanation of window functions, please see the [Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html) topic in our <span class="ItalicFont">Splice Machine Developer's Guide</span>.

See Also

-   [About Data Types](../DataTypes/Intro.NumericTypes.html)
-   [<span class="CodeFont">AVG</span>](CurrentDate.html) function
-   [<span class="CodeFont">COUNT</span>](Count.html) function
-   [<span class="CodeFont">DENSE\_RANK</span>](DenseRank.html) function
-   [<span class="CodeFont">FIRST\_VALUE</span>](FirstValue.html) function
-   [<span class="CodeFont">LAG</span>](Lag.html) function
-   [<span class="CodeFont">LAST\_VALUE</span>](LastValue.html) function
-   [<span class="CodeFont">LEAD</span>](Lead.html) function
-   [<span class="CodeFont">MAX</span>](Max.html) function
-   [<span class="CodeFont">MIN</span>](Min.html) function
-   [<span class="CodeFont">RANK</span>](Rank.html) function
-   [<span class="CodeFont">ROW\_NUMBER</span>](RowNumber.html) function
-   [<span class="CodeFont">SUM</span>](Sum.html) function
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">GROUP BY</span>](../Clauses/GroupBy.html) clause
-   [<span class="CodeFont">HAVING</span>](../Clauses/Having.html) clause
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   <span class="ItalicFont">[Using Window Functions](../../Developers/Fundamentals/UsingWindowFunctions.html)</span> in the <span class="ItalicFont">Developer Guide</span>.

 


