[Open topic with navigation](../../../index.html#Shared/SQLReference/JoinOps/CrossJoin.html)

<a href="" id="SQL-JoinOps.CrossJoin"></a>[]()CROSS JOIN
========================================================

A <span class="CodeFont">CROSS JOIN</span> is a [<span class="CodeFont">JOIN</span> operation](AboutJoins.html) that produces the Cartesian product of two tables. Unlike other <span class="CodeFont">JOIN</span> operators, it does not let you specify a join clause. You may, however, specify a <span class="CodeFont">WHERE</span> clause in the <span class="CodeFont">SELECT</span> statement.

Syntax

``` FcnSyntax
TableExpression CROSS JOIN {
    TableViewOrFunctionExpression | ( TableExpression )
}
```

Examples

The following <span class="CodeFont">SELECT</span> statements are equivalent:

``` Example
splice> SELECT * FROM CITIES CROSS JOIN FLIGHTS;

splice> SELECT * FROM CITIES, FLIGHTS;
```

The following <span class="CodeFont">SELECT</span> statements are equivalent:

``` Example
splice> SELECT * FROM CITIES CROSS JOIN FLIGHTS
   WHERE CITIES.AIRPORT = FLIGHTS.ORIG_AIRPORT;

splice> SELECT * FROM CITIES INNER JOIN FLIGHTS
    ON CITIES.AIRPORT = FLIGHTS.ORIG_AIRPORT;
```

The following example is more complex. The <span class="CodeFont">ON</span> clause in this example is associated with the <span class="CodeFont">LEFT OUTER JOIN</span> operation. Note that you can use parentheses around a <span class="CodeFont">JOIN</span> operation.

``` Example
splice> SELECT * FROM CITIES LEFT OUTER JOIN
  (FLIGHTS CROSS JOIN COUNTRIES)
  ON CITIES.AIRPORT = FLIGHTS.ORIG_AIRPORT
  WHERE COUNTRIES.COUNTRY_ISO_CODE = 'US';
```

A <span class="CodeFont">CROSS JOIN</span> operation can be replaced with an <span class="CodeFont">INNER JOIN</span> where the join clause always evaluates to true (for example, <span class="CodeFont">1=1</span>). It can also be replaced with a sub-query. So equivalent queries would be:

``` Example
splice> SELECT * FROM CITIES LEFT OUTER JOIN 
  FLIGHTS INNER JOIN COUNTRIES ON 1=1
  ON CITIES.AIRPORT = FLIGHTS.ORIG_AIRPORT
  WHERE COUNTRIES.COUNTRY_ISO_CODE = 'US';

splice> SELECT * FROM CITIES LEFT OUTER JOIN
  (SELECT * FROM FLIGHTS, COUNTRIES) S
  ON CITIES.AIRPORT = S.ORIG_AIRPORT
  WHERE S.COUNTRY_ISO_CODE = 'US';
```

See Also

-   [JOIN operations](Intro.JoinOps.html)
-   [<span class="CodeFont">USING</span>](../Clauses/Using.html) clause

 


