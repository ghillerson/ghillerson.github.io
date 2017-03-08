[Open topic with navigation](../../../index.html#Shared/SQLReference/JoinOps/RightOuterJoin.html)

<a href="" id="JoinOps.RightOuterJoin"></a>[]()RIGHT OUTER JOIN
===============================================================

A <span class="CodeFont">RIGHT OUTER JOIN</span> is one of the [<span class="CodeFont">JOIN</span> operations](AboutJoins.html) that allow you to specify a <span class="CodeFont">JOIN</span> clause. It preserves the unmatched rows from the second (right) table, joining them with a <span class="CodeFont">NULL</span> in the shape of the first (left) table. A Right Outer <span class="CodeFont">JOIN B </span>is equivalent to <span class="CodeFont">B RIGHT OUTER JOIN A</span>, with the columns in a different order.

Syntax

``` FcnSyntax
TableExpression RIGHT [ OUTER ] JOIN TableExpression
{
 ON booleanExpression | USING clause
}
```

The scope of expressions in the <span class="CodeFont">ON</span> clause includes the current tables and any tables in query blocks outer to the current <span class="CodeFont">SELECT</span>. The <span class="CodeFont">ON</span> clause can reference tables not being joined and does not have to reference either of the tables being joined (though typically it does).

Example 1

``` Example
   -- get all countries and corresponding cities, including
   -- countries without any cities
splice> SELECT COUNTRIES.COUNTRY, CITIES.CITY_NAME 
  FROM CITIES  RIGHT OUTER JOIN COUNTRIES 
  ON CITIES.COUNTRY_ISO_CODE = COUNTRIES.COUNTRY_ISO_CODE;

   -- get all countries in Africa and corresponding cities,
   -- including countries without any cities
splice> SELECT COUNTRIES.COUNTRY, CITIES.CITY_NAME
  FROM CITIES 
  RIGHT OUTER JOIN COUNTRIES 
  ON CITIES.COUNTRY_ISO_CODE = COUNTRIES.COUNTRY_ISO_CODE
  WHERE Countries.region = 'Africa';

  -- use the synonymous syntax, RIGHT JOIN, to achieve exactly
  -- the same results as in the example above
splice> SELECT COUNTRIES.COUNTRY, CITIES.CITY_NAME
  FROM CITIES 
  RIGHT JOIN COUNTRIES 
  ON CITIES.COUNTRY_ISO_CODE = COUNTRIES.COUNTRY_ISO_CODE
  WHERE Countries.region = 'Africa';
```

Example 2

``` Example
   -- a TableExpression can be a joinOperation. Therefore
   -- you can have multiple join operations in a FROM clause
   -- List every employee number and last name 
   -- with the employee number and last name of their manager
splice> SELECT E.EMPNO, E.LASTNAME, M.EMPNO, M.LASTNAME 
  FROM EMPLOYEE E RIGHT OUTER JOIN  
  DEPARTMENT RIGHT OUTER JOIN EMPLOYEE M 
  ON MGRNO = M.EMPNO
  ON E.WORKDEPT = DEPTNO;
```

See Also

-   [<span class="CodeFont">JOIN</span>](Intro.JoinOps.html) operations
-   [<span class="CodeFont">TABLE</span>](../Expressions/Table.html) expression
-   [<span class="CodeFont">USING</span>](../Clauses/Using.html) clause

 


