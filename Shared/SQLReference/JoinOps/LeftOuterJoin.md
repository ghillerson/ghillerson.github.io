[Open topic with navigation](../../../index.html#Shared/SQLReference/JoinOps/LeftOuterJoin.html)

<a href="" id="JoinOps.LeftOuterJoin"></a>[]()LEFT OUTER JOIN
=============================================================

A <span class="CodeFont">LEFT OUTER JOIN</span> is one of the [<span class="CodeFont">JOIN</span> operations](AboutJoins.html) that allow you to specify a join clause. It preserves the unmatched rows from the first (left) table, joining them with a <span class="CodeFont">NULL</span> row in the shape of the second (right) table.

Syntax

``` FcnSyntax
TableExpression LEFT [ OUTER ] JOIN TableExpression
{
    ON booleanExpression |
    USING clause
}
```

The scope of expressions in either the <span class="CodeFont">ON</span> clause includes the current tables and any tables in query blocks outer to the current <span class="CodeFont">SELECT</span>. The <span class="CodeFont">ON</span> clause can reference tables not being joined and does not have to reference either of the tables being joined (though typically it does).

Example 1

``` Example
   -- match cities to countries in Asia
splice> SELECT CITIES.COUNTRY, CITIES.CITY_NAME, REGION 
  FROM Countries 
  LEFT OUTER JOIN Cities
  ON CITIES.COUNTRY_ISO_CODE = COUNTRIES.COUNTRY_ISO_CODE
  WHERE REGION = 'Asia';

   -- use the synonymous syntax, LEFT JOIN, to achieve exactly 
   -- the same results as in the example above
splice> SELECT  COUNTRIES.COUNTRY, CITIES.CITY_NAME,REGION 
  FROM COUNTRIES 
  LEFT JOIN CITIES 
  ON CITIES.COUNTRY_ISO_CODE = COUNTRIES.COUNTRY_ISO_CODE
  WHERE REGION = 'Asia';
```

Example 2

``` Example
   -- Join the EMPLOYEE and DEPARTMENT tables, 
   -- select the employee number (EMPNO), 
   -- employee surname (LASTNAME), 
   -- department number (WORKDEPT in the EMPLOYEE table
   -- and DEPTNO in the DEPARTMENT table) 
   -- and department name (DEPTNAME) 
   -- of all employees who born (BIRTHDATE) earlier than 1930
splice> SELECT EMPNO, LASTNAME, WORKDEPT, DEPTNAME 
  FROM SAMP.EMPLOYEE LEFT OUTER JOIN SAMP.DEPARTMENT 
  ON WORKDEPT = DEPTNO 
  AND YEAR(BIRTHDATE) < 1930;

   -- List every department with the employee number and 
   -- last name of the manager,
   -- including departments without a manager
splice> SELECT DEPTNO, DEPTNAME, EMPNO, LASTNAME
  FROM DEPARTMENT LEFT OUTER JOIN EMPLOYEE
  ON MGRNO = EMPNO;
```

See Also

-   [<span class="CodeFont">JOIN</span>](Intro.JoinOps.html) operations
-   [<span class="CodeFont">TABLE</span>](../Expressions/Table.html) expression
-   [<span class="CodeFont">USING</span>](../Clauses/Using.html) clause

 


