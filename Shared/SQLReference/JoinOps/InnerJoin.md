[Open topic with navigation](../../../index.html#Shared/SQLReference/JoinOps/InnerJoin.html)

<a href="" id="SQL-JoinOps.InnerJoin"></a>[]()INNER JOIN
========================================================

An <span class="CodeFont">INNER JOIN</span> is a [<span class="CodeFont">JOIN</span> operation](AboutJoins.html) that allows you to specify an explicit join clause.

Syntax

``` FcnSyntax
TableExpression [ INNER ] JOIN TableExpression
  {ON booleanExpression | USING clause}
```

You can specify the join clause by specifying <span class="CodeFont">ON</span> with a boolean expression.

The scope of expressions in the <span class="CodeFont">ON</span> clause includes the current tables and any tables in outer query blocks to the current <span class="CodeFont">SELECT</span>. In the following example, the <span class="CodeFont">ON</span> clause refers to the current tables:

``` Example
SELECT *
  FROM SAMP.EMPLOYEE INNER JOIN SAMP.STAFF
  ON EMPLOYEE.SALARY < STAFF.SALARY;
```

The <span class="CodeFont">ON</span> clause can reference tables not being joined and does not have to reference either of the tables being joined (though typically it does).

Examples

``` Example
   -- Join the EMP_ACT and EMPLOYEE tables 
   -- select all the columns from the EMP_ACT table and 
   -- add the employee's surname (LASTNAME) from the EMPLOYEE table
   -- to each row of the result
splice> SELECT SAMP.EMP_ACT.*, LASTNAME
  FROM SAMP.EMP_ACT JOIN SAMP.EMPLOYEE
  ON EMP_ACT.EMPNO = EMPLOYEE.EMPNO;

   -- Join the EMPLOYEE and DEPARTMENT tables, 
   -- select the employee number (EMPNO), 
   -- employee surname (LASTNAME), 
   -- department number (WORKDEPT in the EMPLOYEE table and DEPTNO in the  
   -- DEPARTMENT table) 
   -- and department name (DEPTNAME) 
   -- of all employees who were born (BIRTHDATE) earlier than 1930.
splice> SELECT EMPNO, LASTNAME, WORKDEPT, DEPTNAME 
  FROM SAMP.EMPLOYEE JOIN SAMP.DEPARTMENT 
  ON WORKDEPT = DEPTNO 
  AND YEAR(BIRTHDATE) < 1930;

   -- Another example of "generating" new data values, 
   -- using a query which selects from a VALUES clause (which is an 
   -- alternate form of a fullselect). 
   -- This query shows how a table can be derived called "X"
   -- having 2 columns "R1" and "R2" and 1 row of data
splice> SELECT *
  FROM (VALUES (3, 4), (1, 5), (2, 6))  
  AS VALUESTABLE1(C1, C2)
  JOIN (VALUES (3, 2), (1, 2),
  (0, 3)) AS VALUESTABLE2(c1, c2) 
  ON VALUESTABLE1.c1 = VALUESTABLE2.c1;
   -- This results in:
   -- C1         |C2         |C1         |2
   -- -----------------------------------------------
   -- 3          |4          |3          |2
   -- 1          |5          |1          |2
  
   -- List every department with the employee number and 
   -- last name of the manager
splice> SELECT DEPTNO, DEPTNAME, EMPNO, LASTNAME
  FROM DEPARTMENT INNER JOIN EMPLOYEE
  ON MGRNO = EMPNO;

   -- List every employee number and last name 
   -- with the employee number and last name of their manager
splice> SELECT E.EMPNO, E.LASTNAME, M.EMPNO, M.LASTNAME 
  FROM EMPLOYEE E INNER JOIN    
  DEPARTMENT INNER JOIN EMPLOYEE M 
  ON MGRNO = M.EMPNO
  ON E.WORKDEPT = DEPTNO;
```

See Also

-   [JOIN operations](Intro.JoinOps.html)
-   [<span class="CodeFont">USING</span>](../Clauses/Using.html) clause

 


