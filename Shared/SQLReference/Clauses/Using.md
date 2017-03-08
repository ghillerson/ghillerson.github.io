[Open topic with navigation](../../../index.html#Shared/SQLReference/Clauses/Using.html)

<a href="" id="Clauses.Using"></a> USING
========================================

The <span class="CodeFont">USING</span> clause specifies which columns to test for equality when two tables are joined. It can be used instead of an <span class="CodeFont">ON</span> clause in <span class="CodeFont">JOIN</span> operations that have an explicit join clause.

Syntax

``` FcnSyntax
USING ( SimpleColumnName [ , Simple-column-Name ]* )
```

SimpleColumnName

The name of a table column, as described in the [Simple Column Name](../Identifiers/IdentifierTypes.html#SimpleColumnName) topic.

Using

The columns listed in the <span class="CodeFont">USING</span> clause must be present in both of the tables being joined. The <span class="CodeFont">USING</span> clause will be transformed to an <span class="CodeFont">ON</span> clause that checks for equality between the named columns in the two tables.

When a <span class="CodeFont">USING</span> clause is specified, an asterisk (<span class="CodeFont">\*</span>) in the select list of the query will be expanded to the following list of columns (in this order):

-   All the columns in the <span class="CodeFont">USING</span> clause
-   All the columns of the first (left) table that are not specified in the <span class="CodeFont">USING</span> clause
-   All the columns of the second (right) table that are not specified in the <span class="CodeFont">USING</span> clause

An asterisk qualified by a table name (for example, <span class="Example">COUNTRIES.\*</span>) will be expanded to every column of that table that is not listed in the <span class="CodeFont">USING</span> clause.

If a column in the <span class="CodeFont">USING</span> clause is referenced without being qualified by a table name, the column reference points to the column in the first (left) table if the join is an <span class="CodeFont">[INNER JOIN](../JoinOps/InnerJoin.html)</span> or a <span class="CodeFont">[LEFT OUTER JOIN](../JoinOps/LeftOuterJoin.html)</span>. If it is a <span class="CodeFont">[RIGHT OUTER JOIN](../JoinOps/RightOuterJoin.html)</span>, unqualified references to a column in the <span class="CodeFont">USING</span> clause point to the column in the second (right) table.

Examples

The following query performs an inner join between the <span class="CodeFont">COUNTRIES</span> table and the <span class="CodeFont">CITIES</span> table on the condition that <span class="CodeFont">COUNTRIES.COUNTRY</span> is equal to <span class="CodeFont">CITIES.COUNTRY</span>:

``` Example
SELECT * FROM COUNTRIES JOIN CITIES
   USING (COUNTRY);
```

The next query is similar to the one above, but it has the additional join condition that <span class="CodeFont">COUNTRIES.COUNTRY\_ISO\_CODE</span> is equal to <span class="CodeFont">CITIES.COUNTRY\_ISO\_CODE</span>:

``` Example
SELECT * FROM COUNTRIES JOIN CITIES
   USING (COUNTRY, COUNTRY_ISO_CODE);
```

See Also

-   [Join Operations](../JoinOps/Intro.JoinOps.html)
-   [<span class="CodeFont">SELECT</span>](../Statements/Select.html) statement

 


