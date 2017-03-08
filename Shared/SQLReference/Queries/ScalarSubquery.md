[Open topic with navigation](../../../index.html#Shared/SQLReference/Queries/ScalarSubquery.html)

<a href="" id="Queries.ScalarSubquery"></a>[]()Scalar Subquery
==============================================================

A <span class="ItalicFont">ScalarSubquery</span> turns a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html)</span> result into a scalar value because it returns only a single row and column value.

Syntax

``` FcnSyntax
( Query
  [ ORDER BY clause ]
  [ result offset clause ]
  [ fetch first clause ]
)
```

Usage

You can place a <span class="ItalicFont">ScalarSubquery</span> anywhere an <span class="ItalicFont">Expression</span> is permitted. The query must evaluate to a single row with a single column.

Scalar subqueries are also called <span class="ItalicFont">expression subqueries</span>.

Examples

The <span class="CodeFont">AVG</span> function always returns a single value; thus, this is a scalar subquery:

``` Example
SELECT NAME, COMM
  FROM STAFF
  WHERE EXISTS
    (SELECT AVG(BONUS + 800)
       FROM EMPLOYEE
       WHERE COMM < 5000
       AND EMPLOYEE.LASTNAME = UPPER(STAFF.NAME)
    );

   -- Introduce a way of "generating" new data values,
   -- using a query which selects from a VALUES clause (which is 
   -- an alternate form of a fullselect). 
   -- This query shows how a table can be derived called "X" 
   -- having 2 columns "R1" and "R2" and 1 row of data.
 SELECT R1,R2 
   FROM (VALUES('GROUP 1','GROUP 2')) AS MYTBL(R1,R2);
```

This example derives a table named <span class="CodeFont">MYTBL</span> by using the <span class="CodeFont">VALUES</span> clause to populate the table:

``` Example
 SELECT R1,R2 
   FROM (VALUES('GROUP 1','GROUP 2')) AS MYTBL(R1,R2);
```

See Also

-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression

 


