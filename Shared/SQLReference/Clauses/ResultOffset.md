[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/ResultOffset.html)

<a href="" id="Clauses.ResultOffset"></a>[]()RESULT OFFSET and []()FETCH FIRST
==============================================================================

The <span class="ItalicFont">result offset clause</span> provides a way to skip the N first rows in a result set before starting to return any rows.

The <span class="ItalicFont">fetch first clause</span>, which can be combined with the <span class="ItalicFont">result offset clause</span>, limits the number of rows returned in the result set. The <span class="ItalicFont">fetch first clause</span> can sometimes be useful for retrieving only a few rows from an otherwise large result set, usually in combination with an <span class="CodeFont">ORDER BY</span> clause. Use of this clause can increase efficienty and make programming simpler.

Syntax

``` FcnSyntax
OFFSET { integer-literal | ? }
       {ROW | ROWS}
```

integer-literal

An integer value that specifies the number of rows to skip. The default value is <span class="CodeFont">0</span>.

If non-zero, this must be a positive integer value. If you specify a value greater than the number of rows in the underlying result set, no rows are returned.

 

``` FcnSyntax
FETCH { FIRST | NEXT } 
   [integer-literal | ? ]
   {ROW | ROWS} ONLY
```

integer-literal

An integer value that specifies the maximum number of rows to return in the result set. The default value is <span class="CodeFont">1</span>.

This must be a positive integer value greater than or equal to <span class="CodeFont">1</span>.

Usage

Note that:

-   <span class="CodeFont">ROW</span> and <span class="CodeFont">ROWS</span> are synonymous
-   <span class="CodeFont">FIRST</span> and <span class="CodeFont">NEXT</span> are synonymous

Be sure to specify the <span class="CodeFont">ORDER BY</span> clause if you expect to retrieve a sorted result set.

Examples

``` Example
   -- Fetch the first row of T
SELECT * FROM T FETCH FIRST ROW ONLY;

   -- Sort T using column I, then fetch rows 11 through 20
   --   of the sorted rows (inclusive)
SELECT * FROM T ORDER BY I 
         OFFSET 10 ROWS
         FETCH NEXT 10 ROWS ONLY;

   -- Skip the first 100 rows of T
   -- If the table has fewer than 101 records, 
   --   an empty result set is returned
SELECT * FROM T OFFSET 100 ROWS;

   -- Use of ORDER BY and FETCH FIRST in a subquery
SELECT DISTINCT A.ORIG_AIRPORT, B.FLIGHT_ID FROM 
   (SELECT FLIGHT_ID, ORIG_AIRPORT 
       FROM FLIGHTS 
       ORDER BY ORIG_AIRPORT DESC 
       FETCH FIRST 40 ROWS ONLY) 
    AS A, FLIGHTAVAILABILITY AS B 
   WHERE A.FLIGHT_ID = B.FLIGHT_ID;

   -- JDBC (using a dynamic parameter):
PreparedStatement p = 
   con.prepareStatement("SELECT * FROM T 
                         ORDER BY I 
                         OFFSET ? ROWS");
   p.setInt(1, 100);
ResultSet rs = p.executeQuery();
```

See Also

-   <span class="CodeFont">[LIMIT n](Limit.html)</span> clause
-   [<span class="CodeFont">SELECT</span>](../Statements/Select.html) statement
-   <span class="CodeFont">[TOP n](TopN.html)</span> clause

 


