[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/Insert.html)

<a href="" id="Statements.Insert"></a>[]()INSERT
================================================

An <span class="CodeFont">INSERT</span> statement creates rows or columns and stores them in the named table. The number of values assigned in an <span class="CodeFont">INSERT</span> statement must be the same as the number of specified or implied columns.

Whenever you insert into a table which has generated columns, Splice Machine calculates the values of those columns.

Syntax

``` FcnSyntax
INSERT INTO table-Name
   [ (Simple-column-Name [ , Simple-column-Name]* ) ]
   Query [ ORDER BY clause ]
   [ result offset clause ]
   [ fetch first clause ];
```

table-Name

The table into which you are inserting data.

Simple-column-Name\*

An optional list of names of the columns to populate with data.

Query \[ORDER BY clause\]

A <span class="CodeFont">SELECT</span> or <span class="CodeFont">VALUES</span> command that provides the columns and rows of data to insert. The query can also be a <span class="CodeFont">UNION</span> expression.

See the [Using the <span class="CodeFont">ORDER BY</span> Clause](#OrderBy) section below for information about using the <span class="CodeFont">ORDER BY</span> clause.

Single-row and multiple-row <span class="CodeFont">VALUES</span> expressions can include the keyword <span class="CodeFont">DEFAULT</span>. Specifying <span class="CodeFont">DEFAULT</span> for a column inserts the column's default value into the column. Another way to insert the default value into the column is to omit the column from the column list and only insert values into other columns in the table. For more information, see [<span class="CodeFont">VALUES</span> expression](../Expressions/Values.html)

result offset and fetch first clauses

The [<span class="CodeFont">result offset</span> clause](../Clauses/ResultOffset.html) provides a way to skip the N first rows in a result set before starting to data to the table. The [<span class="CodeFont">fetch first</span> clause](../Clauses/ResultOffset.html), which can be combined with the <span class="CodeFont">result offset</span> clause, limits the number of rows added to the table.

[]()Using the ORDER BY Clause

When you want insertion to happen with a specific ordering (for example, in conjunction with auto-generated keys), it can be useful to specify an <span class="CodeFont">ORDER BY</span> clause on the result set to be inserted.

If the Query is a <span class="CodeFont">VALUES</span> expression, it cannot contain or be followed by an <span class="CodeFont">ORDER BY</span>, result offset, or fetch first clause. However, if the <span class="CodeFont">VALUES</span> expression does not contain the <span class="CodeFont">DEFAULT</span> keyword, the <span class="CodeFont">VALUES</span> clause can be put in a subquery and ordered, as in the following statement:

``` Example
INSERT INTO t SELECT * FROM (VALUES 'a','c','b') t ORDER BY 1;
```

For more information about queries, see [Query](../Queries/Query.html).

Examples

These examples insert records with literal values:

``` Example
splice> INSERT INTO Players
   VALUES( 99, 'Giants', 'Joe Bojangles', 'C', 'Little Joey', '07/11/91');
1 row inserted/updated/deleted

splice> INSERT INTO Players
   VALUES( (99, 'Giants', 'Joe Bojangles', 'C', 'Little Joey', '07/11/91'),
           (73, 'Giants', 'Lester Johns', 'P', 'Big John', '06/09/84'),
           (27, 'Cards', 'Earl Hastings', 'OF', 'Speedy Earl', '04/22/82') );
3 rows inserted/updated/deleted
```

This example creates a table name OldGuys that has the same columns as our Players table, and then loads that table with the data from Players for all players born before 1980:

``` Example
splice> CREATE TABLE OldGuys(
    ID           SMALLINT NOT NULL PRIMARY KEY,
    Team         VARCHAR(64) NOT NULL,
    Name         VARCHAR(64) NOT NULL,
    Position     CHAR(2),
    DisplayName  VARCHAR(24),
    BirthDate    DATE
    );

splice> INSERT INTO OldGuys
   SELECT * FROM Players 
   WHERE BirthDate < '01/01/1980';
```

Statement dependency system

The <span class="CodeFont">INSERT</span> statement depends on the table being inserted into, all of the conglomerates (units of storage such as heaps or indexes) for that table, and any other table named in the statement. Any statement that creates or drops an index or a constraint for the target table of a prepared <span class="CodeFont">INSERT</span> statement invalidates the prepared <span class="CodeFont">INSERT</span> statement.

See Also

-   [<span class="CodeFont">FETCH FIRST</span>](../Clauses/ResultOffset.html) clause
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause
-   [Queries](../Queries/Query.html)
-   [<span class="CodeFont">RESULT OFFSET</span>](../Clauses/ResultOffset.html) clause

 


