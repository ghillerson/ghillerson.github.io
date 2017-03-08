[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/With.html)

[]()WITH CLAUSE (Common Table Expression)
=========================================

You can use Common Table Expressions, also known as the <span class="CodeFont">WITH</span> clause, to break down complicated queries into simpler parts by naming and referring to subqueries within queries.

A Common Table Expression (CTE) provides a way of defining a temporary result set whose definition is available only to the query in which the CTE is defined. The result of the CTE is not stored; it exists only for the duration of the query. CTEs are helpful in reducing query complexity and increasing readability. They can be used as substitutions for views in cases where either you don’t have permission to create a view or the query would be the only one using the view. CTEs allow you to more easily enable grouping by a column that is derived from a scalar sub select or a function that is non deterministic.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The <span class="CodeFont">WITH</span> clause is also known as the <span class="ItalicFont">subquery factoring clause</span>.

The handling and syntax of <span class="CodeFont">WITH</span> queries are similar to the handling and syntax of views. The <span class="CodeFont">WITH</span> clause can be processed as an inline view and shares syntax with <span class="CodeFont">CREATE VIEW</span>. The <span class="CodeFont">WITH</span> clause can also resolve as a temporary table, which may enhance the efficiency of a query.

Syntax

``` FcnSyntax
WITH queryName 
   AS SELECT SelectExpr
SELECT Query
```

queryName

An identifier that names the subquery clause.

Examples

If we create the following table:

``` Example
CREATE TABLE BANKS (
       INSTITUTION_ID INTEGER NOT NULL,
       INSTITUTION_NAME VARCHAR(100),
       CITY VARCHAR(100),
       STATE VARCHAR(2),
       TOTAL_ASSETS DECIMAL(19,2),
       NET_INCOME DECIMAL(19,2),
       OFFICES INTEGER,
       PRIMARY KEY(INSTITUTION_ID)
);
```

We can then use a common table expression to improve the readability of a statement that finds the per-city total assets and income for the states with the top net income:

``` Example
WITH state_sales AS (
       SELECT STATE, SUM(NET_INCOME) AS total_sales
       FROM INSTITUTIONS
       GROUP BY STATE
   ), top_states AS (
       SELECT STATE
       FROM state_sales
       WHERE total_sales > (SELECT SUM(total_sales)/10 FROM state_sales)
   )
SELECT STATE,
       CITY,
       SUM(TOTAL_ASSETS) AS assets,
       SUM(NET_INCOME) AS income
FROM INSTITUTIONS
WHERE STATE IN (SELECT STATE FROM top_states)
GROUP BY STATE, CITY;
```

See Also

-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">Query</span>](../Queries/Query.html) 

WITH

 


