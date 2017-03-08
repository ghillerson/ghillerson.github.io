[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/Select.html)

<a href="" id="Expressions.Select"></a>[]()SELECT Expression
============================================================

A <span class="ItalicFont">SelectExpression</span> is the basic <span class="CodeFont">SELECT-FROM-WHERE</span> construct used to build a table value based on filtering and projecting values from other tables.

Syntax

``` FcnSyntax
SELECT [ DISTINCT | ALL ] SelectItem [ , SelectItem ]*
   FROM clause
   [ WHERE clause]
   [ GROUP BY clause ]
   [ HAVING clause ]
   [ ORDER BY clause ]
   [ result offset clause ]
   [ fetch first clause ]
```

SELECT clause

The <span class="CodeFont">SELECT</span> clause contains a list of expressions and an optional quantifier that is applied to the results of the [<span class="CodeFont">FROM</span> clause](../Clauses/From.html) and the [<span class="CodeFont">WHERE</span> clause](../Clauses/Where.html).

If <span class="CodeFont">DISTINCT</span> is specified, only one copy of any row value is included in the result. Nulls are considered duplicates of one another for the purposes of <span class="CodeFont">DISTINCT</span>.

If no quantifier, or <span class="CodeFont">ALL</span>, is specified, no rows are removed from the result in applying the <span class="CodeFont">SELECT</span> clause. This is the default behavior.

SelectItem:

``` FcnSyntax
{
    * |
    { table-Name | correlation-Name } .* |
      Expression [AS Simple-column-Name] }
}
```

A<span class="ItalicFont"> SelectItem</span> projects one or more result column values for a table result being constructed in a <span class="ItalicFont">SelectExpression</span>.

For queries that do not select a specific column from the tables involved in the <span class="ItalicFont">SelectExpression</span> (for example, queries that use COUNT(\*)), the user must have at least one column-level SELECT privilege or table-level SELECT privilege. See [GRANT statement](../Statements/Grant.html) for more information.

FROM clause

The result of the [<span class="CodeFont">FROM</span> clause](../Clauses/From.html) is the cross product of the <span class="CodeFont">FROM</span> items.

WHERE clause

The [<span class="CodeFont">WHERE</span> clause](../Clauses/Where.html) can further qualify the result of the <span class="CodeFont">FROM</span> clause.

GROUP BY clause

The [<span class="CodeFont">GROUP BY</span> clause](../Clauses/Where.html) groups rows in the result into subsets that have matching values for one or more columns.

<span class="CodeFont">GROUP BY</span> clauses are typically used with aggregates. If there is a <span class="CodeFont">GROUP BY</span> clause, the <span class="CodeFont">SELECT</span> clause must contain <span class="ItalicFont">only</span> aggregates or grouping columns. If you want to include a non-grouped column in the <span class="CodeFont">SELECT</span> clause, include the column in an aggregate expression. For example, this query computes the average salary of each team in a baseball league:

``` Example
splice> SELECT COUNT(*) AS PlayerCount, Team, AVG(Salary) AS AverageSalary
   FROM Players JOIN Salaries ON Players.ID=Salaries.ID 
   GROUP BY Team 
   ORDER BY AverageSalary;
```

If there is no <span class="CodeFont">GROUP BY</span> clause, but a <span class="ItalicFont">SelectItem</span> contains an aggregate not in a subquery, the query is implicitly grouped. The entire table is the single group.

HAVING clause

The [<span class="CodeFont">HAVING</span> clause](../Clauses/Having.html) can further qualify the result of the <span class="CodeFont">FROM</span> clause. This clause restricts a grouped table, specifying a search condition (much like a <span class="CodeFont">WHERE</span> clause) that can refer only to grouping columns or aggregates from the current scope.

The <span class="CodeFont">HAVING</span> clause is applied to each group of the grouped table. If the <span class="CodeFont">HAVING</span> clause evaluates to <span class="CodeFont">TRUE</span>, the row is retained for further processing; if it evaluates to <span class="CodeFont">FALSE</span> or <span class="CodeFont">NULL</span>, the row is discarded. If there is a <span class="CodeFont">HAVING</span> clause but no <span class="CodeFont">GROUP BY</span>, the table is implicitly grouped into one group for the entire table.

ORDER BY clause

The [<span class="CodeFont">ORDER BY</span> clause](../Clauses/OrderBy.html) allows you to specify the order in which rows appear in the result set. In subqueries, the <span class="CodeFont">ORDER BY</span> clause is meaningless unless it is accompanied by one or both of the result offset and fetch first clauses.

<span class="CodeItalicFont">result offset</span> and <span class="CodeItalicFont">fetch first</span> clauses

The [<span class="CodeFont">result offset</span> clause](../Clauses/ResultOffset.html) provides a way to skip the N first rows in a result set before starting to return any rows. The [<span class="CodeFont">fetch first</span> clause](../Clauses/ResultOffset.html), which can be combined with the <span class="CodeFont">result offset</span> clause, limits the number of rows returned in the result set.

Usage

The result of a <span class="ItalicFont">SelectExpression</span> is always a table.

Splice Machine processes the clauses in a <span class="CodeFont">Select</span> expression in the following order:

-   <span class="CodeFont">FROM</span> clause
-   <span class="CodeFont">WHERE</span> clause
-   <span class="CodeFont">GROUP BY</span> (or implicit <span class="CodeFont">GROUP BY</span>)
-   <span class="CodeFont">HAVING</span> clause
-   <span class="CodeFont">ORDER BY</span> clause
-   <span class="CodeFont">Result offset</span> clause
-   <span class="CodeFont">Fetch first</span> clause
-   <span class="CodeFont">SELECT</span> clause

When a query does not have a <span class="CodeFont">FROM</span> clause (when you are constructing a value, not getting data out of a table), use a <span class="CodeFont">[VALUES](Values.html)</span> expression, not a <span class="ItalicFont">SelectExpression</span>. For example:

``` Example
VALUES CURRENT_TIMESTAMP;
```

<a href="" id="StarWildcard"></a>The \* wildcard

The wildcard character (<span class="ItalicFont">\*</span>) expands to all columns in the tables in the associated <span class="CodeFont">FROM</span> clause.

<span class="ItalicFont">[table-Name](../Identifiers/IdentifierTypes.html#TableName).\*</span> and <span class="ItalicFont">[correlation-Name](../Identifiers/IdentifierTypes.html#CorrelationName).\*</span> expand to all columns in the identified table. That table must be listed in the associated <span class="CodeFont">FROM</span> clause.

Naming columns

You can name a <span class="ItalicFont">SelectItem</span> column using the <span class="CodeFont">AS</span> clause.

If a column of a <span class="ItalicFont">SelectItem</span> is not a simple <span class="ItalicFont">ColumnReference</span> expression or named with an <span class="CodeFont">AS</span> clause, it is given a generated unique name.

These column names are useful in several cases:

-   They are made available on the JDBC <span class="ItalicFont">ResultSetMetaData</span>.
-   They are used as the names of the columns in the resulting table when the <span class="ItalicFont">SelectExpression</span> is used as a table subquery in a <span class="CodeFont">FROM</span> clause.
-   They are used in the <span class="CodeFont">ORDER BY</span> clause as the column names available for sorting.

Examples

This example shows using a <span class="CodeFont">SELECT</span> with <span class="CodeFont">WHERE</span> and <span class="CodeFont">ORDER BY</span> clauses; it selects the name, team, and birth date of all players born in 1985 and 1989:

``` Example
splice> SELECT DisplayName, Team, BirthDate 
   FROM Players 
   WHERE YEAR(BirthDate) IN (1985, 1989) 
   ORDER BY BirthDate;
DISPLAYNAME             |TEAM      |BIRTHDATE 
-----------------------------------------------
Jeremy Johnson          |Cards     |1985-03-15
Gary Kosovo             |Giants    |1985-06-12
Michael Hillson         |Cards     |1985-11-07
Mitch Canepa            |Cards     |1985-11-26
Edward Erdman           |Cards     |1985-12-21
Jeremy Packman          |Giants    |1989-01-01
Nathan Nickels          |Giants    |1989-05-04
Ken Straiter            |Cards     |1989-07-20
Marcus Bamburger        |Giants    |1989-08-01
George Goomba           |Cards     |1989-08-08
Jack Hellman            |Cards     |1989-08-09
Elliot Andrews          |Giants    |1989-08-21
Henry Socomy            |Giants    |1989-11-17

13 rows selected
```

This example shows using correlation names for the tables:

``` Example
splice> SELECT CONSTRAINTNAME, COLUMNNAME 
  FROM SYS.SYSTABLES t, SYS.SYSCOLUMNS col,
  SYS.SYSCONSTRAINTS cons, SYS.SYSCHECKS checks 
  WHERE t.TABLENAME = 'FLIGHTS' 
    AND t.TABLEID = col.REFERENCEID 
    AND t.TABLEID = cons.TABLEID 
    AND cons.CONSTRAINTID = checks.CONSTRAINTID 
  ORDER BY CONSTRAINTNAME;
```

This example shows using the <span class="CodeFont">DISTINCT</span> clause:

``` Example
 SELECT DISTINCT SALARY
   FROM Salaries;
```

This example shows how to rename an expression. We use the name BOSS as the maximum department salary for all departments whose maximum salary is less than the average salary i all other departments:

``` Example
 SELECT WORKDEPT AS DPT, MAX(SALARY) AS BOSS 
   FROM EMPLOYEE EMP_COR 
   GROUP BY WORKDEPT 
   HAVING MAX(SALARY) <
     (SELECT AVG(SALARY)
      FROM EMPLOYEE
      WHERE NOT WORKDEPT = EMP_COR.WORKDEPT) 
   ORDER BY BOSS;
```

See Also

-   [<span class="CodeFont">FROM</span>](../Clauses/From.html) clause
-   [<span class="CodeFont">GROUP BY</span>](../Clauses/GroupBy.html) clause
-   [<span class="CodeFont">HAVING</span>](../Clauses/Having.html) clause
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   [<span class="CodeFont">WHERE</span>](../Clauses/Where.html) clause

 


