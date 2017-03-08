[Open topic with navigation](../../../index.html#Shared/SQLReference/Expressions/Table.html)

<a href="" id="Expressions.Table"></a>[]()TABLE Expression
==========================================================

A <span class="ItalicFont">TableExpression</span> specifies a table, view, or function in a [<span class="CodeFont">FROM</span> clause](../Clauses/From.html). It is the source from which a <span class="ItalicFont">[TableExpression](#)</span> selects a result.

Syntax

``` FcnSyntax
{
   TableViewOrFunctionExpression | JOIN operations
}
```

Usage

A correlation name can be applied to a table in a <span class="ItalicFont">TableExpression</span> so that its columns can be qualified with that name.

-   If you do not supply a correlation name, the table name qualifies the column name.
-   When you give a table a correlation name, you cannot use the table name to qualify columns.
-   You must use the correlation name when qualifying column names.
-   No two items in the <span class="CodeFont">FROM</span> clause can have the same correlation name, and no correlation name can be the same as an unqualified table name specified in that <span class="CodeFont">FROM</span> clause.

In addition, you can give the columns of the table new names in the <span class="CodeFont">AS</span> clause. Some situations in which this is useful:

-   When a [<span class="CodeFont">VALUES</span> expression](Values.html) is used as a <span class="ItalicFont">[TableSubquery](../Queries/TableSubquery.html),</span> since there is no other way to name the columns of a <span class="CodeFont">VALUES</span> expression.
-   When column names would otherwise be the same as those of columns in other tables; renaming them means you don't have to qualify them.

The Query in a <span class="ItalicFont">[TableSubquery](../Queries/TableSubquery.html)</span> appearing in a <span class="ItalicFont">FromItem</span> can contain multiple columns and return multiple rows. See <span class="ItalicFont">[TableSubquery](../Queries/TableSubquery.html).</span>

Example

``` Example
   -- SELECT from a JOIN expression
SELECT E.EMPNO, E.LASTNAME, M.EMPNO, M.LASTNAME
  FROM EMPLOYEE E LEFT OUTER JOIN
       DEPARTMENT INNER JOIN EMPLOYEE M 
       ON MGRNO = M.EMPNO
       ON E.WORKDEPT = DEPTNO;
```

<a href="" id="TableViewExpression"></a>TableViewOrFunctionExpression

``` FcnSyntax
{
   { table-Name | view-Name }
   [ CorrelationClause ]  |
   { TableSubquery | TableFunctionInvocation }
   CorrelationClause
}
```

where <span class="ItalicFont">CorrelationClause</span> is

``` FcnSyntax
[ AS ]
correlation-Name
[ ( Simple-column-Name [ , Simple-column-Name ]* ) ] 
```

<a href="" id="TableFunction"></a>TableFunctionExpression

``` FcnSyntax
{
  TABLE function-name( [ [ function-arg ] [, function-arg ]* ] )
}
```

Note that when you invoke a table function, you must bind it to a correlation name. For example:

``` Example
splice> SELECT s.* FROM TABLE( externalEmployees( 42 ) ) s;
```

See Also

-   [<span class="CodeFont">FROM</span>](../Clauses/From.html) clause
-   [<span class="CodeFont">JOIN</span>](../JoinOps/AboutJoins.html) operations
-   [<span class="CodeFont">SELECT</span>](../Statements/Select.html) statement
-   [<span class="CodeFont">VALUES</span>](Values.html) expression

 


