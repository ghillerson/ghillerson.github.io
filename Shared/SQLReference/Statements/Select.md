[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/Select.html)

<a href="" id="Statements.Select"></a>[]()SELECT
================================================

Use the <span class="CodeFont">SELECT</span> statement to query a database and receive back results.

Syntax

``` FcnSyntax
SELECT Query  
   [ORDER BY clause]
   [result offset clause]
   [fetch first clause]
```

Query

The <span class="CodeFont">SELECT</span> statement is so named because the typical first word of the query construct is <span class="CodeFont">SELECT</span>. (<span class="ItalicFont">Query</span> includes the <span class="CodeFont">[VALUES](../Expressions/Values.html)</span> and <span class="CodeFont">UNION</span> expressions as well as <span class="CodeFont">[SELECT](../Expressions/Select.html)</span> expressions).

ORDER BY clause

The <span class="CodeFont">[ORDER BY](../Clauses/OrderBy.html)</span> clause allows you to order the results of the <span class="CodeFont">SELECT</span>. Without the <span class="CodeFont">ORDER BY</span> clause, the results are returned in random order.

result offset and fetch first clauses

The [<span class="CodeFont">result offset</span> clause](../Clauses/ResultOffset.html) provides a way to skip the N first rows in a result set before starting to fetch results. The [<span class="CodeFont">fetch first</span> clause](../Clauses/ResultOffset.html), which can be combined with the <span class="CodeFont">result offset</span> clause, limits the number of rows fetched.

Example

This examples selects all records in the Players table:

``` Example
splice> SELECT * FROM Players WHERE ID < 11;
ID    |TEAM     |POS&|DISPLAYNAME        |BIRTHDATE 
------------------------------------------------------
1     |Giants   |C   |Buddy Painter      |1987-03-27
2     |Giants   |1B  |Billy Bopper       |1988-04-20
3     |Giants   |2B  |John Purser        |1990-10-30
4     |Giants   |SS  |Bob Cranker        |1987-01-21
5     |Giants   |3B  |Mitch Duffer       |1991-01-15
6     |Giants   |LF  |Norman Aikman      |1982-01-05
7     |Giants   |CF  |Alex Paramour      |1981-07-02
8     |Giants   |RF  |Harry Pennello     |1983-04-13
9     |Giants   |OF  |Greg Brown         |1983-12-24
10    |Giants   |RF  |Jason Minman       |1983-11-06

10 rows selected
```

This examples select the Birthdate of all players born in November or December:

``` Example
splice> SELECT BirthDate 
   FROM Players 
   WHERE MONTH(BirthDate) > 10 
   ORDER BY BIRTHDATE;
BIRTHDATE 
----------
1980-12-19
1983-11-06
1983-11-28
1983-12-24
1984-11-22
1985-11-07
1985-11-26
1985-12-21
1986-11-13
1986-11-24
1986-12-16
1987-11-12
1987-11-16
1987-12-17
1988-12-21
1989-11-17
1991-11-15

17 rows selected
```

This example selects the name, team, and birth date of all players born in 1985 and 1989:

``` Example
splice> SELECT DisplayName, Team, BirthDate 
   FROM Players 
   WHERE YEAR(BirthDate) IN (1985, 1989) 
   ORDER BY BirthDate;
DISPLAYNAME             |TEAM      |BIRTHDATE 
-----------------------------------------------
Jeremy Johnson          |Cards     |1985-03-15
Gary Kosovo             |Giants    |1985-06-12
Michael Hillson         |Cards     |1985-11-07
Mitch Canepa            |Cards     |1985-11-26
Edward Erdman           |Cards     |1985-12-21
Jeremy Packman          |Giants    |1989-01-01
Nathan Nickels          |Giants    |1989-05-04
Ken Straiter            |Cards     |1989-07-20
Marcus Bamburger        |Giants    |1989-08-01
George Goomba           |Cards     |1989-08-08
Jack Hellman            |Cards     |1989-08-09
Elliot Andrews          |Giants    |1989-08-21
Henry Socomy            |Giants    |1989-11-17

13 rows selected
```

Statement dependency system

The <span class="CodeFont">SELECT</span> statement depends on all the tables and views named in the query and the conglomerates (units of storage such as heaps and indexes) chosen for access paths on those tables. <span class="CodeFont">[CREATE INDEX](CreateIndex.html)</span> does not invalidate a prepared <span class="CodeFont">SELECT</span> statement. A <span class="CodeFont">[DROP INDEX](DropIndex.html)</span> statement invalidates a prepared <span class="CodeFont">SELECT</span> statement if the index is an access path in the statement. If the <span class="CodeFont">SELECT</span> includes views, it also depends on the dictionary objects on which the view itself depends (see [<span class="CodeFont">CREATE VIEW</span> statement](CreateView.html)).

The <span class="CodeFont">SELECT</span> statements depends on all aliases used in the query. Dropping an alias invalidates any prepared <span class="CodeFont">SELECT</span> statement that uses the alias.

See Also

-   [<span class="CodeFont">CREATE INDEX</span>](CreateIndex.html)statement
-   [<span class="CodeFont">CREATE VIEW</span>](CreateView.html)statement
-   [<span class="CodeFont">DROP INDEX</span>](DropIndex.html)statement
-   [<span class="CodeFont">DROP VIEW</span>](DropView.html)statement
-   [<span class="CodeFont">GRANT</span>](Grant.html)statement
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html)clause
-   [<span class="CodeFont">FETCH FIRST</span>](../Clauses/ResultOffset.html)clause
-   [<span class="CodeFont">RESULT OFFSET</span>](../Clauses/ResultOffset.html)clause

 


