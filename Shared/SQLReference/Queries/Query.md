[Open topic with navigation](../../../index.html#Shared/SQLReference/Queries/Query.html)

<a href="" id="SQL-Queries.Query"></a>[]()Query
===============================================

A <span class="ItalicFont">Query</span> creates a virtual table based on existing tables or constants built into tables.

Syntax

``` FcnSyntax
{
  ( Query
       [ ORDER BY clause ]
       [ result offset clause ]
       [ fetch first clause ] 
  ) |
   Query EXCEPT [ ALL | DISTINCT ] Query |
   Query UNION [ ALL | DISTINCT ] Query |
   SelectExpression | VALUES Expression
}
```

You can arbitrarily put parentheses around queries, or use the parentheses to control the order of evaluation of the <span class="CodeFont">UNION</span> operations. These operations are evaluated from left to right when no parentheses are present.

Duplicates in UNION and EXCEPT ALL results

The <span class="CodeFont">ALL</span> and <span class="CodeFont">DISTINCT</span> keywords determine whether duplicates are eliminated from the result of the operation. If you specify the <span class="CodeFont">DISTINCT</span> keyword, then the result will have no duplicate rows. If you specify the <span class="CodeFont">ALL</span> keyword, then there may be duplicates in the result, depending on whether there were duplicates in the input. <span class="CodeFont">DISTINCT</span> is the default, so if you don't specify <span class="CodeFont">ALL</span> or <span class="CodeFont">DISTINCT</span>, the duplicates will be eliminated. For example, <span class="CodeFont">UNION</span> builds an intermediate <span class="ItalicFont">ResultSet</span> with all of the rows from both queries and eliminates the duplicate rows before returning the remaining rows. <span class="CodeFont">UNION ALL</span> returns all rows from both queries as the result.

Depending on which operation is specified, if the number of copies of a row in the left table is L and the number of copies of that row in the right table is R, then the number of duplicates of that particular row that the output table contains (assuming the <span class="CodeFont">ALL</span> keyword is specified) is:

-   <span class="CodeFont">UNION</span>: ( L + R ).
-   <span class="CodeFont">EXCEPT</span>: the maximum of ( L - R ) and 0 (zero).

Examples

Here's a simple <span class="CodeFont">SELECT</span> expression:

``` Example
SELECT *
  FROM ORG;
```

Here's a <span class="CodeFont">SELECT</span> with a subquery:

``` Example
SELECT *    
  FROM (SELECT CLASS_CODE FROM CL_SCHED) AS CS;
```

Here's a <span class="CodeFont">SELECT</span> with a subquery:

``` Example
SELECT *    
  FROM (SELECT CLASS_CODE FROM CL_SCHED) AS CS;
```

Here's a <span class="CodeFont">UNION</span> that lists all employee numbers from certain departments who are assigned to specified project numbers:

``` Example
SELECT EMPNO, 'emp'
  FROM EMPLOYEE
  WHERE WORKDEPT LIKE 'E%'
  UNION   
    SELECT EMPNO, 'emp_act'
       FROM EMP_ACT
       WHERE PROJNO IN('MA2100', 'MA2110', 'MA2112');
```

See Also

-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">SELECT</span>](../Statements/Select.html) statement
-   [<span class="CodeFont">VALUES</span>](../Expressions/Values.html) expression

 


