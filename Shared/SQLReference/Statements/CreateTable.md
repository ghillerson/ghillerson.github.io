[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateTable.html)

<a href="" id="Statements.CreateTable"></a>[]()CREATE TABLE
===========================================================

A <span class="CodeFont">CREATE TABLE</span> statement creates a table. Tables contain columns and constraints, rules to which data must conform. Table-level constraints specify a column or columns. Columns have a data type and can specify column constraints (column-level constraints).

The table owner and the database owner automatically gain the following privileges on the table and are able to grant these privileges to other users:

-   INSERT
-   SELECT
-   TRIGGER
-   UPDATE

These privileges cannot be revoked from the table and database owners.

For information about constraints, see [<span class="CodeFont">CONSTRAINT</span> clause](../Clauses/Constraint.html).

You can specify a default value for a column. A default value is the value to be inserted into a column if no other value is specified. If not explicitly specified, the default value of a column is <span class="CodeFont">NULL</span>.

If a qualified table name is specified, the schema name cannot begin with <span class="CodeFont">SYS</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The [CREATE EXTERNAL TABLE](CreateExternalTable.html) and [PIN TABLE](PinTable.html) statements are documented separately in this section.

Syntax

There are two different variants of the <span class="CodeFont">CREATE TABLE</span> statement, depending on whether you are specifying the column definitions and constraints, or whether you are modeling the columns after the results of a query expression with the <span class="CodeFont">CREATE TABLE AS</span> form:

``` FcnSyntax
CREATE TABLE table-Name
  {
      ( {column-definition |
         Table-level constraint}
         [ , {column-definition} ] * 
      )
  |
      [ ( column-name [ , column-name ] * ) ]
      AS query-expression [AS <name>]
      WITH NO DATA
   }
```

table-Name

The name to assign to the new table.

column-definition

A column definition.

The maximum number of columns allowed in a table is <span class="CodeFont"><span class="LimitationsMaxColumnsInTable">100000</span></span>.

Table-level constraint

A constraint that applies to the table.

column-name

A column definition.

AS query-expression

See the <span class="CodeFont">[CREATE TABLE AS](#createAs)</span> section below.

If this select list contains an expression, you must name the result of the expression. Refer to the final example at the bottom of this topic page.

WITH NO DATA

See the <span class="CodeFont">[CREATE TABLE AS](#createAs)</span> section below.

[]()CREATE TABLE ... AS ...

With this alternate form of the <span class="CodeFont">CREATE TABLE</span> statement, the column names and/or the column data types can be specified by providing a query. The columns in the query result are used as a model for creating the columns in the new table.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="BoldFont">You cannot include</span> an <span class="CodeFont">ORDER BY</span> clause in the query expression you use in the <span class="CodeFont">CREATE TABLE AS</span> statement.
If the select list contains an expression, <span class="BoldFont">you must name the result of the expression</span>. Refer to the final example at the bottom of this topic page.

If no column names are specified for the new table, then all the columns in the result of the query expression are used to create same-named columns in the new table, of the corresponding data type(s). If one or more column names are specified for the new table, then the same number of columns must be present in the result of the query expression; the data types of those columns are used for the corresponding columns of the new table.

The <span class="CodeFont">WITH NO DATA</span> clause specifies that the data rows which result from evaluating the query expression are not used; only the names and data types of the columns in the query result are used.

> There is currently a known problem using the <span class="CodeFont">CREATE TABLE AS</span> form of the <span class="CodeFont">CREATE TABLE</span> statement .when the data to be inserted into the new table results from a <span class="CodeFont">RIGHT OUTER JOIN</span> operation. For example, the following statement currently produces a table with all <span class="CodeFont">NULL</span> values:
>
> ``` Example
> splice> CREATE TABLE t3 AS
>    SELECT t1.a,t1.b,t2.c,t2.d
>    FROM t1 RIGHT OUTER JOIN t2 ON t1.b = t2.c
>    WITH DATA;
> 0 rows inserted/updated/deleted
> ```
>
> There's a simple workaround for now: create the table without inserting the data, and then insert the data; for example:
>
> ``` Example
> splice> CREATE TABLE t3 AS
>    SELECT t1.a,t1.b,t2.c,t2.d
>    FROM t1 RIGHT OUTER JOIN t2 ON t1.b = t2.c
>    WITH NO DATA;
> 0 rows inserted/updated/deleted
>
> splice> INSERT INTO t3
>    SELECT t1.a,t1.b,t2.c,t2.d 
>    FROM t1 RIGHT OUTER JOIN t2 ON t1.b = t2.c;
> 0 rows inserted/updated/deleted
> ```
>
Examples

This section presents examples of both forms of the <span class="CodeFont">CREATE TABLE</span> statement.

CREATE TABLE

This example creates our Players table:

``` Example
splice> CREATE TABLE Players(
    ID           SMALLINT NOT NULL PRIMARY KEY,
    Team         VARCHAR(64) NOT NULL,
    Name         VARCHAR(64) NOT NULL,
    Position     CHAR(2),
    DisplayName  VARCHAR(24),
    BirthDate    DATE
    );
0 rows inserted/updated/deleted
```

This example includes a table-level primary key definition that includes two columns:

``` Example
splice> CREATE TABLE HOTELAVAILABILITY (
   Hotel_ID INT NOT NULL,
   BookingDate DATE NOT NULL,
   Rooms_Taken INT DEFAULT 0,
   PRIMARY KEY (Hotel_ID, Booking_Date );
0 rows inserted/updated/deleted
```

This example assigns an identity column attribute with an initial value of 5 that increments by 5, and also includes a primary key constraint:

``` Example
splice> CREATE TABLE PEOPLE (
   Person_ID INT NOT NULL GENERATED ALWAYS AS IDENTITY (START WITH 5, INCREMENT BY 5)
      CONSTRAINT People_PK PRIMARY KEY,
   Person VARCHAR(26) );
0 rows inserted/updated/deleted
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>For more examples of <span class="CodeFont">CREATE TABLE</span> statements using the various constraints, see [<span class="CodeFont">CONSTRAINT</span> clause](../Clauses/Constraint.html)

CREATE TABLE AS

This example creates a new table that uses all of the columns (and their data types) from an existing table, but does not duplicate the data:

``` Example
splice> CREATE TABLE NewPlayers
   AS SELECT * 
         FROM Players WITH NO DATA;
0 rows inserted/updated/deleted
```

This example creates a new table that includes the data and uses only some of the columns from an existing table, and assigns new names for the columns:

``` Example
splice> CREATE TABLE MorePlayers (ID, PlayerName, Born)
   AS SELECT ID, DisplayName, Birthdate
         FROM Players WITH DATA;
94 rows inserted/updated/deleted
```

This example creates a new table using unnamed expressions in the query and shows that the data types are the same for the corresponding columns in the newly created table:

``` Example
splice> CREATE TABLE T3 (X,Y)
   AS SELECT 2*I AS COL1, 2.0*F AS COL2
         FROM T1 WITH NO DATA;
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">ALTER TABLE</span>](AlterTable.html) statement
-   [<span class="CodeFont">CREATE EXTERNAL TABLE</span>](CreateExternalTable.html) statement
-   [<span class="CodeFont">PIN TABLE</span>](PinTable.html) statement
-   [<span class="CodeFont">CONSTRAINT</span>](../Clauses/Constraint.html) clause
-   <span class="CodeFont">[DROP TABLE](DropTable.html)</span> statement
-   [<span class="CodeFont">UNPIN TABLE</span>](UnpinTable.html) statement
-   [Foreign Keys](../../Developers/Fundamentals/ForeignKeys.html) in the <span class="ItalicFont">Developer's Guide</span>.
-   [Triggers](../../Developers/Fundamentals/DatabaseTriggers.html) in the <span class="ItalicFont">Developer's Guide</span>.

 


