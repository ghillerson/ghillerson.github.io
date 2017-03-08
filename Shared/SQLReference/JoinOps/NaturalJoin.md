[Open topic with navigation](../../../index.html#Shared/SQLReference/JoinOps/NaturalJoin.html)

<a href="" id="JoinOps.NaturalJoin"></a>[]()NATURAL JOIN
========================================================

A <span class="CodeFont">NATURAL JOIN</span> is a [<span class="CodeFont">JOIN</span> operation](AboutJoins.html) that creates an implicit join clause for you based on the common columns in the two tables being joined. Common columns are columns that have the same name in both tables.

Syntax

``` FcnSyntax
TableExpression NATURAL 
   [ { LEFT | RIGHT } 
     [ OUTER ] | INNER ] JOIN
   { TableViewOrFunctionExpression | 
     ( TableExpression ) }
```

Usage

A <span class="CodeFont">NATURAL JOIN</span> can be an <span class="CodeFont">INNER</span> join, a <span class="CodeFont">LEFT OUTER</span> join, or a <span class="CodeFont">RIGHT OUTER</span> join. The default is <span class="CodeFont">INNER</span> join.

If the <span class="CodeFont">SELECT</span> statement in which the <span class="CodeFont">NATURAL JOIN</span> operation appears has an asterisk (<span class="CodeFont">\*</span>) in the select list, the asterisk will be expanded to the following list of columns (in the shown order):

-   All the common columns
-   Every column in the first (left) table that is not a common column
-   Every column in the second (right) table that is not a common column

An asterisk qualified by a table name (for example, <span class="CodeFont">COUNTRIES.\*</span>) will be expanded to every column of that table that is not a common column.

If a common column is referenced without being qualified by a table name, the column reference points to the column in the first (left) table if the join is an <span class="CodeFont">INNER JOIN</span> or a <span class="CodeFont">LEFT OUTER JOIN</span>. If it is a <span class="CodeFont">RIGHT OUTER JOIN</span>, unqualified references to a common column point to the column in the second (right) table.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine does not currently support <span class="CodeFont">NATURAL SELF JOIN</span> operations.

Examples

If the tables <span class="CodeFont">COUNTRIES</span> and <span class="CodeFont">CITIES</span> have two common columns named <span class="CodeFont">COUNTRY</span> and <span class="CodeFont">COUNTRY\_ISO\_CODE</span>, the following two <span class="CodeFont">SELECT</span> statements are equivalent:

``` Example
splice> SELECT * 
  FROM COUNTRIES 
  NATURAL JOIN CITIES;

splice> SELECT * 
  FROM COUNTRIES 
  JOIN CITIES
  USING (COUNTRY, COUNTRY_ISO_CODE);
```

The following example is similar to the one above, but it also preserves unmatched rows from the first (left) table:

``` Example
splice> SELECT * 
  FROM COUNTRIES 
  NATURAL LEFT JOIN CITIES;
```

See Also

-   [<span class="CodeFont">JOIN</span>](Intro.JoinOps.html) operations
-   [<span class="CodeFont">TABLE</span>](../Expressions/Table.html) expression
-   [<span class="CodeFont">USING</span>](../Clauses/Using.html) clause

 


