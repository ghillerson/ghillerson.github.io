[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Having.html)

<a href="" id="Clauses.Having"></a>[]()HAVING
=============================================

A <span class="CodeFont">HAVING</span> clause restricts the results of a [<span class="CodeFont">GROUP BY</span>](GroupBy.html) clause in a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html).</span>

The <span class="CodeFont">HAVING</span> clause is applied to each group of the grouped table, similarly to how a <span class="CodeFont">[WHERE](Where.html)</span> clause is applied to a select list.

If there is no <span class="CodeFont">GROUP BY</span> clause, the <span class="CodeFont">HAVING</span> clause is applied to the entire result as a single group. The <span class="CodeFont">[SELECT](../Statements/Select.html)</span> expression cannot refer directly to any column that does not have a <span class="CodeFont">GROUP BY</span> clause. It can, however, refer to constants, aggregates, and special registers.

Syntax

``` FcnSyntax
HAVING searchCondition
```

searchCondition

A specialized Boolean expression, as described in the next section.

Using

The <span class="ItalicFont">searchCondition</span>, is a specialized <span class="ItalicFont">[booleanExpression](../Expressions/BooleanExpressions.html)</span> that can contain only;

-   grouping columns (see [<span class="CodeFont">GROUP BY</span>](GroupBy.html) clause)
-   columns that are part of aggregate expressions
-   columns that are part of a subquery

For example, the following query is illegal, because the column <span class="CodeFont">SALARY</span> is not a grouping column, it does not appear within an aggregate, and it is not within a subquery:

``` Example
SELECT COUNT(*)
  FROM SAMP.STAFF
  GROUP BY ID
  HAVING SALARY > 15000;
```

Aggregates in the <span class="CodeFont">HAVING</span> clause do not need to appear in the <span class="CodeFont">SELECT</span> list. If the <span class="CodeFont">HAVING</span> clause contains a subquery, the subquery can refer to the outer query block if and only if it refers to a grouping column.

Example

``` Example
   -- Find the total number of economy seats taken on a flight,
   -- grouped by airline,
   -- only when the group has at least 2 records.
SELECT SUM(ECONOMY_SEATS_TAKEN), AIRLINE_FULL
  FROM FLIGHTAVAILABILITY, AIRLINES
  WHERE SUBSTR(FLIGHTAVAILABILITY.FLIGHT_ID, 1, 2) = AIRLINE
  GROUP BY AIRLINE_FULL
  HAVING COUNT(*) > 1;
```

See Also

-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">GROUP BY</span>](GroupBy.html) clause
-   [<span class="CodeFont">WHERE</span>](Where.html) clause

 


