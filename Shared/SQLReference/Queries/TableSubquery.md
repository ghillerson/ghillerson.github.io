[Open topic with navigation](../../../index.html#Shared/SQLReference/Queries/TableSubquery.html)

<a href="" id="Queries.TableSubquery"></a>[]()Table Subquery
============================================================

A <span class="ItalicFont">TableSubquery</span> is a subquery that returns multiple rows.

Syntax

``` FcnSyntax
( Query
    [ ORDER BY clause ]
    [ result offset clause ]
    [ fetch first clause ]
)
```

Usage

Unlike a <span class="ItalicFont">[ScalarSubquery](ScalarSubquery.html),</span> a <span class="ItalicFont">TableSubquery</span> is allowed only:

-   as a <span class="ItalicFont">[TableExpression](../Expressions/Table.html)</span> in a [<span class="CodeFont">FROM</span> clause](../Clauses/From.html)
-   with <span class="CodeFont">EXISTS</span>, <span class="CodeFont">IN</span>, or quantified comparisons.

When used as a <span class="ItalicFont">[TableExpression](../Expressions/Table.html)</span> in a [<span class="CodeFont">FROM</span> clause](../Clauses/From.html), or with <span class="CodeFont">EXISTS</span>, it can return multiple columns.

When used with <span class="CodeFont">IN</span> or quantified comparisons, it must return a single column.

Example

This example shows a subquery used as a table expression in a <span class="CodeFont">FROM</span> clause:

``` Example
SELECT VirtualFlightTable.flight_ID 
  FROM
     (SELECT flight_ID, orig_airport, dest_airport
        FROM Flights
        WHERE (orig_airport = 'SFO' OR dest_airport = 'SCL')
      )
  AS VirtualFlightTable;
```

This shows one subquery used with <span class="CodeFont">EXISTS</span> and another used with <span class="CodeFont">IN</span>:

``` Example
SELECT *
  FROM Flights
  WHERE EXISTS
    (SELECT *
       FROM Flights
       WHERE dest_airport = 'SFO'
       AND orig_airport = 'GRU');

SELECT flight_id, segment_number
  FROM Flights
  WHERE flight_id IN
    (SELECT flight_ID
       FROM Flights
       WHERE orig_airport = 'SFO'
       OR dest_airport = 'SCL');
```

See Also

-   [<span class="CodeFont">FROM</span>](../Clauses/From.html) clause
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">TABLE</span>](../Expressions/Table.html) expression

 


