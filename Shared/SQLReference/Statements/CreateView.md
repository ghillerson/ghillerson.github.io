[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateView.html)

<a href="" id="Statements.CreateView"></a>[]()CREATE VIEW
=========================================================

Views are virtual tables formed by a query. A view is a dictionary object that you can use until you drop it. Views are not updatable.

If a qualified view name is specified, the schema name cannot begin with <span class="ItalicFont">SYS</span>.

Syntax

``` FcnSyntax
CREATE VIEW view-Name
   [ ( Simple-column-Name [, Simple-column-Name] * ) ]
   AS Query [ ORDER BY clause ]
     [ RESULT OFFSET clause ]
     [ FETCH FIRST clause ] 
```

A view definition can contain an optional view column list to explicitly name the columns in the view. If there is no column list, the view inherits the column names from the underlying query. All columns in a view must be uniquely named.

view-Name

The name to assign to the view.

Simple-column-Name\*

An optional list of names to be used for columns of the view. If not given, the column names are deduced from the query.

The maximum number of columns in a view is <span class="CodeFont"><span class="LimitationsMaxColumnsInView">5000</span></span>.

AS Query \[ORDER BY clause\]

A <span class="CodeFont">SELECT</span> or <span class="CodeFont">VALUES</span> command that provides the columns and rows of the view.

result offset and fetch first clauses

The [<span class="CodeFont">RESULT OFFSET</span> clause](../Clauses/ResultOffset.html) provides a way to skip the N first rows in a result set before starting to add rows to the view. The [<span class="CodeFont">FETCH FIRST</span> clause](../Clauses/ResultOffset.html), which can be combined with the <span class="CodeFont">RESULT OFFSET</span> clause, limits the number of rows added to the view.

Examples

This example creates a view that shows the age of each player in our database:

``` Example
splice> CREATE VIEW PlayerAges (Player, Team, Age) 
   AS SELECT DisplayName, Team, 
      INT( (Now - Birthdate) / 365.25) AS Age 
      FROM Players;
0 rows inserted/updated/deleted

splice> SELECT * FROM PlayerAges WHERE Age > 30 ORDER BY Team, Age DESC;
PLAYER                  |TEAM     |AGE        
-----------------------------------------
Robert Cohen            |Cards    |40         
Jason Larrimore         |Cards    |37         
David Janssen           |Cards    |36         
Mitch Hassleman         |Cards    |35         
Mitch Brandon           |Cards    |35         
Tam Croonster           |Cards    |34         
Alex Wister             |Cards    |34         
Yuri Milleton           |Cards    |33         
Jonathan Pearlman       |Cards    |33         
Michael Rastono         |Cards    |32         
Barry Morse             |Cards    |32         
Carl Vanamos            |Cards    |32         
Jan Bromley             |Cards    |31         
Thomas Hillman          |Giants   |40         
Mark Briste             |Giants   |38         
Randy Varner            |Giants   |38         
Jason Lilliput          |Giants   |38         
Jalen Ardson            |Giants   |36         
Sam Castleman           |Giants   |35         
Alex Paramour           |Giants   |34         
Jack Peepers            |Giants   |34         
Norman Aikman           |Giants   |33         
Craig McGawn            |Giants   |33         
Kameron Fannais         |Giants   |33         
Jason Martell           |Giants   |33         
Harry Pennello          |Giants   |32         
Jason Minman            |Giants   |32         
Trevor Imhof            |Giants   |32         
Steve Raster            |Giants   |32         
Greg Brown              |Giants   |31         
Alex Darba              |Giants   |31         
Joseph Arkman           |Giants   |31         
Tam Lassiter            |Giants   |31         
Martin Cassman          |Giants   |31         
Yuri Piamam             |Giants   |31         

35 rows selected
```

Statement Dependency System

View definitions are dependent on the tables and views referenced within the view definition. DML (data manipulation language) statements that contain view references depend on those views, as well as the objects in the view definitions that the views are dependent on. Statements that reference the view depend on indexes the view uses; which index a view uses can change from statement to statement based on how the query is optimized. For example, given:

``` Example
splice> CREATE TABLE T1 (C1 DOUBLE PRECISION);
0 rows inserted/updated/deleted

splice>CREATE FUNCTION SIN (DATA DOUBLE) 
   RETURNS DOUBLE  
   EXTERNAL NAME 'java.lang.Math.sin'
   LANGUAGE JAVA PARAMETER STYLE JAVA;
0 rows inserted/updated/deleted

splice> CREATE VIEW V1 (C1) AS SELECT SIN(C1) FROM T1;
0 rows inserted/updated/deleted
```

The following <span class="CodeFont">SELECT</span>:

``` Example
SELECT * FROM V1;
```

Is dependent on view <span class="ItalicFont">V1</span>, table <span class="ItalicFont">T1,</span> and external scalar function <span class="ItalicFont">SIN.</span>

See Also

-   [<span class="CodeFont">DROP VIEW</span>](DropView.html) statement
-   [<span class="CodeFont">ORDER BY</span>](../Clauses/OrderBy.html) clause

 


