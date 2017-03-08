[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Where.html)

<a href="" id="Clauses.Where"></a>[]()WHERE
===========================================

The <span class="CodeFont">WHERE</span> clause is an optional part of a <span class="CodeFont">[SelectExpression](../Expressions/Select.html)</span>, a <span class="CodeFont">[DELETE](../Statements/Delete.html)</span> statement, or an <span class="CodeFont">[UPDATE](../Statements/UpdateTable.html)</span> statement.

The <span class="CodeFont">WHERE</span> clause lets you select rows based on a Boolean expression. Only rows for which the expression evaluates to <span class="CodeFont">TRUE</span> are selected to return or operate upon (delete or update).

Syntax

``` FcnSyntax
WHERE BooleanExpression
```

BooleanExpression

A Boolean expression. For more information, see the [Boolean Expressions](../Expressions/BooleanExpressions.html) topic.

Example

``` Example
   -- find the flights where no business-class seats have been booked     
SELECT *
  FROM FlightAvailability
  WHERE business_seats_taken IS NULL
     OR business_seats_taken = 0;

   -- Join the EMP_ACT and EMPLOYEE tables
   -- select all the columns from the EMP_ACT table and 
   -- add the employee's surname (LASTNAME) from the EMPLOYEE table 
   -- to each row of the result.
SELECT SAMP.EMP_ACT.*, LASTNAME
  FROM SAMP.EMP_ACT, SAMP.EMPLOYEE
  WHERE EMP_ACT.EMPNO = EMPLOYEE.EMPNO;


   -- Determine the employee number and salary of sales representatives 
   -- along with the average salary and head count of their departments.
   -- This query must first create a new-column-name specified in the AS clause 
   -- which is outside the fullselect (DINFO) 
   -- in order to get the AVGSALARY and EMPCOUNT columns, 
   -- as well as the DEPTNO column that is used in the WHERE clause
SELECT THIS_EMP.EMPNO, THIS_EMP.SALARY, DINFO.AVGSALARY, DINFO.EMPCOUNT
  FROM EMPLOYEE THIS_EMP,
     (SELECT OTHERS.WORKDEPT AS DEPTNO,
           AVG(OTHERS.SALARY) AS AVGSALARY,
           COUNT(*) AS EMPCOUNT
        FROM EMPLOYEE OTHERS
        GROUP BY OTHERS.WORKDEPT
      )AS DINFO
  WHERE THIS_EMP.JOB = 'SALESREP'
    AND THIS_EMP.WORKDEPT = DINFO.DEPTNO;
```

See Also

-   [<span class="CodeFont">Select</span>](../Expressions/Select.html) expressions
-   [<span class="CodeFont">DELETE</span>](../Statements/Delete.html) statement
-   [<span class="CodeFont">SELECT</span>](../Statements/Select.html) statement
-   [<span class="CodeFont">UPDATE</span>](../Statements/UpdateTable.html) statement

 


