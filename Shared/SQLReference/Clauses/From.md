[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/From.html)

<a href="" id="Clauses.From"></a>[]()FROM
=========================================

The <span class="CodeFont">FROM</span> clause is a mandatory clause in a <span class="ItalicFont">[SelectExpression](../Expressions/Select.html).</span> It specifies the tables (<span class="ItalicFont">[TableExpression](../Expressions/Table.html)</span>) from which the other clauses of the query can access columns for use in expressions.

Syntax

``` FcnSyntax
FROM TableExpression [ , TableExpression ] *
```

TableExpression

Specifies a table, view, or function; it is the source from which a <span class="ItalicFont">[TableExpression](../Expressions/Table.html)</span> selects a result.

Examples

``` Example
SELECT Cities.city_id
  FROM Cities
  WHERE city_id < 5;

    -- other types of TableExpressions
  SELECT TABLENAME, ISINDEX 
  FROM SYS.SYSTABLES T, SYS.SYSCONGLOMERATES C
  WHERE T.TABLEID = C.TABLEID
  ORDER BY TABLENAME, ISINDEX;

    -- force the join order
  SELECT *
  FROM Flights, FlightAvailability
  WHERE FlightAvailability.flight_id = Flights.flight_id
   AND FlightAvailability.segment_number = Flights.segment_number
   AND Flights.flight_id < 'AA1115';

   -- a TableExpression can be a joinOperation. Therefore
   -- you can have multiple join operations in a FROM clause
  SELECT COUNTRIES.COUNTRY, CITIES.CITY_NAME,
     FLIGHTS.DEST_AIRPORT
  FROM COUNTRIES LEFT OUTER JOIN CITIES
  ON COUNTRIES.COUNTRY_ISO_CODE = CITIES.COUNTRY_ISO_CODE
  LEFT OUTER JOIN FLIGHTS
  ON Cities.AIRPORT = FLIGHTS.DEST_AIRPORT;
```

See Also

-   [<span class="CodeFont">SELECT</span>](../Expressions/Select.html) expression
-   [<span class="CodeFont">TABLE</span>](../Expressions/Table.html) expression

 


