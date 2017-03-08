[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/OrderBy.html)

<a href="" id="Clauses.OrderBy"></a>[]()ORDER BY
================================================

The <span class="CodeFont">ORDER BY</span> clause is an optional element of the following:

-   A [<span class="CodeFont">SELECT</span> statement](../Statements/Select.html)
-   A <span class="ItalicFont">[SelectExpression](../Expressions/Select.html)</span>
-   A [<span class="CodeFont">VALUES</span> expression](../Expressions/Values.html)
-   A <span class="ItalicFont">[ScalarSubquery](../Queries/ScalarSubquery.html)</span>
-   A <span class="ItalicFont">[TableSubquery](../Queries/TableSubquery.html)</span>

It can also be used in an <span class="CodeFont">[INSERT](../Statements/Insert.html)</span> statement or a <span class="CodeFont">[CREATE VIEW](../Statements/CreateView.html)</span> statement.

An <span class="CodeFont">ORDER BY</span> clause allows you to specify the order in which rows appear in the result set. In subqueries, the <span class="CodeFont">ORDER BY</span> clause is meaningless unless it is accompanied by one or both of the <span class="CodeFont">result offset</span> and <span class="CodeFont">fetch first</span> clauses or in conjunction with the <span class="CodeFont">ROW\_NUMBER</span> function, since there is no guarantee that the order is retained in the outer result set. It is permissible to combine <span class="CodeFont">ORDER BY</span> on the outer query with <span class="CodeFont">ORDER BY</span> in subqueries.

Syntax

``` FcnSyntax
ORDER BY { column-Name |
           ColumnPosition | 
           Expression }
    [ ASC | DESC ]
    [ , column-Name | ColumnPosition | Expression 
      [ ASC | DESC ]
      [ NULLS FIRST | NULLS LAST ]
    ]* 
```

column-Name

A column name, as described in the <span class="CodeFont">[Column Name](../Identifiers/IdentifierTypes.html#ColumnName)</span> topic. This refers to the names visible from the SelectItems in the underlying query of the <span class="CodeFont">[SELECT](../Statements/Select.html)</span> statement. The column name(s) that you specify in the <span class="CodeFont">ORDER BY</span> clause do not need to be the <span class="CodeFont">SELECT</span> list.

ColumnPosition

An integer that identifies the number of the column in the SelectItems in the underlying query of the <span class="CodeFont">SELECT</span> statement. <span class="CodeFont">ColumnPosition</span> must be greater than 0 and not greater than the number of columns in the result table. In other words, if you want to order by a column, that column must be specified in the <span class="CodeFont">SELECT</span> list.

Expression

A sort key expression, such as numeric, string, and datetime expressions. <span class="ItalicFont">Expression</span> can also be a row value expression such as a scalar subquery or case expression.

ASC

Specifies that the results should be returned in ascending order. If the order is not specified, <span class="CodeFont">ASC</span> is the default.

DESC

Specifies that the results should be returned in descending order.

NULLS FIRST

Specifies that <span class="CodeFont">NULL</span> values should be returned before non-<span class="CodeFont">NULL</span> values. This is the default value for descending (<span class="CodeFont">DESC</span>) order.

NULLS LAST

Specifies that <span class="CodeFont">NULL</span> values should be returned after non-<span class="CodeFont">NULL</span> values. This is the default value for ascending (<span class="CodeFont">ASC</span>) order.

Using

If <span class="CodeFont">SELECT DISTINCT</span> is specified or if the <span class="CodeFont">SELECT</span> statement contains a <span class="CodeFont">GROUP BY</span> clause, the <span class="CodeFont">ORDER BY</span> columns must be in the <span class="CodeFont">SELECT</span> list.

Example using a correlation name

You can sort the result set by a correlation name, if the correlation name is specified in the select list. For example, to return from the <span class="CodeFont">CITIES</span> database all of the entries in the <span class="CodeFont">CITY\_NAME</span> and <span class="CodeFont">COUNTRY</span> columns, where the <span class="CodeFont">COUNTRY</span> column has the correlation name <span class="CodeFont">NATION</span>, you specify this <span class="CodeFont">SELECT</span> statement:

``` Example
SELECT CITY_NAME, COUNTRY AS NATION 
  FROM CITIES 
  ORDER BY NATION;
```

Example using a numeric expression

You can sort the result set by a numeric expression, for example:

``` Example
SELECT name, salary, bonus FROM employee 
  ORDER BY salary+bonus;
```

In this example, the salary and bonus columns are <span class="CodeFont">DECIMAL</span> data types.

Example using a function

You can sort the result set by invoking a function, for example:

``` Example
SELECT i, len FROM measures 
  ORDER BY sin(i);
```

Example of specifying a NULL ordering

You can sort the result set by invoking a function, for example:

``` Example
SELECT * FROM Players
  ORDER BY BirthDate DESC NULLS LAST;
```

See Also

-   [<span class="CodeFont">GROUP BY</span>](GroupBy.html) clause
-   [<span class="CodeFont">WHERE</span>](Where.html) clause
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">VALUES</span>](../Expressions/Values.html) expression
-   [<span class="CodeFont">CREATE VIEW</span>](../Statements/CreateView.html) statement
-   [<span class="CodeFont">INSERT</span>](../Statements/Insert.html) statement
-   [<span class="CodeFont">SELECT</span>](../Statements/Select.html) statement

 


