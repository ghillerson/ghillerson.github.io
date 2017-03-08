[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/Values.html)

<a href="" id="Expressions.Values"></a>[]()VALUES Expression
============================================================

The <span class="CodeFont">VALUES</span> expression allows construction of a row or a table from other values.

Syntax

``` FcnSyntax
{
    VALUES ( Value {, Value }* )
        [ , ( Value {, Value }* ) ]* |
    VALUES Value [ , Value ]*
} [ ORDER BY clause ]
  [ result offset clause ]
  [ fetch first clause ]
```

Value

``` FcnSyntax
Expression | DEFAULT
```

The first form constructs multi-column rows. The second form constructs single-column rows, each expression being the value of the column of the row.

The <span class="CodeFont">DEFAULT</span> keyword is allowed only if the <span class="CodeFont">VALUES</span> expression is in an <span class="CodeFont">INSERT</span> statement. Specifying <span class="CodeFont">DEFAULT</span> for a column inserts the column's default value into the column. Another way to insert the default value into the column is to omit the column from the column list and only insert values into other columns in the table.

ORDER BY clause

The [<span class="CodeFont">ORDER BY</span> clause](../Clauses/OrderBy.html) allows you to specify the order in which rows appear in the result set.

result offset and fetch first clauses

The [<span class="CodeFont">result offset</span> clause](../Clauses/ResultOffset.html) provides a way to skip the N first rows in a result set before starting to return any rows. The [<span class="CodeFont">fetch first</span> clause](../Clauses/ResultOffset.html), which can be combined with the <span class="CodeFont">result offset</span> clause, limits the number of rows returned in the result set.

Usage

A <span class="CodeFont">VALUES</span> expression can be used in all the places where a query can, and thus can be used in any of the following ways:

-   As a statement that returns a <span class="ItalicFont">ResultSet</span>
-   Within expressions and statements wherever subqueries are permitted
-   As the source of values for an <span class="CodeFont">[INSERT](../Statements/Insert.html)</span> statement (in an <span class="CodeFont">INSERT</span> statement, you normally use a <span class="CodeFont">VALUES</span> expression when you do not use a <span class="ItalicFont">[SelectExpression](Select.html)</span>)

A <span class="CodeFont">VALUES</span> expression that is used in an <span class="CodeFont">INSERT</span> statement cannot use an <span class="CodeFont">ORDER BY</span> clause. However, if the <span class="CodeFont">VALUES</span> expression does not contain the <span class="CodeFont">DEFAULT</span> keyword, the <span class="CodeFont">VALUES</span> clause can be put in a subquery and ordered, as in the following statement:

``` Example
INSERT INTO t SELECT * FROM (VALUES 'a','c','b') t ORDER BY 1;
```

Examples

``` Example
   -- 3 rows of 1 column
splice> VALUES (1),(2),(3);

   -- 3 rows of 1 column
splice> VALUES 1, 2, 3;

   -- 1 row of 3 columns
splice> VALUES (1, 2, 3);

   -- 3 rows of 2 columns
splice> VALUES (1,21),(2,22),(3,23);

   -- using ORDER BY and FETCH FIRST
splice> VALUES (3,21),(1,22),(2,23) ORDER BY 1 FETCH FIRST 2 ROWS ONLY;

   -- using ORDER BY and OFFSET
splice> VALUES (3,21),(1,22),(2,23) ORDER BY 1 OFFSET 1 ROW;

   -- constructing a derived table
splice> VALUES ('orange', 'orange'), ('apple', 'red'), ('banana', 'yellow');

   -- Insert two new departments using one statement into the DEPARTMENT table, 
   -- but do not assign a manager to the new department.
splice> INSERT INTO DEPARTMENT (DEPTNO, DEPTNAME, ADMRDEPT)
  VALUES ('B11', 'PURCHASING', 'B01'),
    ('E41', 'DATABASE ADMINISTRATION', 'E01');

   -- insert a row with a DEFAULT value for the MAJPROJ column
splice> INSERT INTO PROJECT (PROJNO, PROJNAME, DEPTNO, RESPEMP, PRSTDATE, MAJPROJ) 
VALUES ('PL2101', 'ENSURE COMPAT PLAN', 'B01', '000020', CURRENT_DATE, DEFAULT);

   -- using a built-in function
splice> VALUES CURRENT_DATE;

   -- getting the value of an arbitrary expression
splice> VALUES (3*29, 26.0E0/3);

   -- getting a value returned by a built-in function
splice> values char(1);
```

See Also

-   [<span class="CodeFont">FROM</span>](../Clauses/From.html) clause
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   [<span class="CodeFont">INSERT</span>](../Statements/Insert.html) statement

 


