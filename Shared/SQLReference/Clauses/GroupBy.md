[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/GroupBy.html)

<a href="" id="Clauses.GroupBy"></a>[]()GROUP BY
================================================

A <span class="CodeFont">GROUP BY</span> clause is part of a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html),</span> that groups a result into subsets that have matching values for one or more columns. In each group, no two rows have the same value for the grouping column or columns. NULLs are considered equivalent for grouping purposes.

You typically use a <span class="CodeFont">GROUP BY</span> clause in conjunction with an aggregate expression.

Using the <span class="CodeFont">ROLLUP</span> syntax, you can specify that multiple levels of grouping should be computed at once.

Syntax

``` FcnSyntax
GROUP BY 
  {
  column-Name [ , column-Name ]*  |
  ROLLUP ( column-Name 
       [ , column-Name ]* )
  }
```

column-Name

Must name a column from the current scope of the query; there can be no columns from a query block outside the current scope. For example, if a <span class="CodeFont">GROUP BY</span> clause is in a subquery, it cannot refer to columns in the outer query.

Usage Notes

<span class="ItalicFont">SelectItems</span> in the <span class="ItalicFont">[SelectExpression](../Expressions/Select.html)</span> with a <span class="CodeFont">GROUP BY</span> clause must contain only aggregates or grouping columns.

Examples

``` Example
   -- find the average flying_times of flights grouped by airport
SELECT AVG (flying_time), orig_airport
  FROM Flights
  GROUP BY orig_airport;


SELECT MAX(city_name), region
  FROM Cities, Countries
  WHERE Cities.country_ISO_code = Countries.country_ISO_code
  GROUP BY region;

   -- group by an a smallint
SELECT ID, AVG(SALARY)
  FROM SAMP.STAFF
  GROUP BY ID;

   -- Get the AVGSALARY and EMPCOUNT columns, and the DEPTNO column using the AS clause
   -- And group by the WORKDEPT column using the correlation name OTHERS
SELECT OTHERS.WORKDEPT AS DEPTNO,
     AVG(OTHERS.SALARY) AS AVGSALARY,
     COUNT(*) AS EMPCOUNT
  FROM SAMP.EMPLOYEE OTHERS
  GROUP BY OTHERS.WORKDEPT;

   -- Compute sub-totals of Sales_History data, grouping it by Region, by
   -- (Region, State), and by (Region, State, Product), as well as computing
   -- an overall total of the sales for all Regions, States, and Products:
SELECT Region, State, Product, SUM(Sales) Total_Sales
  FROM Sales_History 
  GROUP BY ROLLUP(Region, State, Product);
```

See Also

-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression

 


