[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateIndex.html)

<a href="" id="Statements.CreateIndex"></a>[]()CREATE INDEX
===========================================================

A <span class="CodeFont">CREATE INDEX</span> statement creates an index on a table. Indexes can be on one or more columns in the table.

Syntax

``` FcnSyntax
CREATE [UNIQUE] INDEX indexName
   ON tableName(
      simpleColumnName
      [ ASC  | DESC ]
      [ , simpleColumnName [ ASC | DESC ]] * 
     )
```

indexName

An identifier, the length of which cannot exceed 128 characters.

tableName

A table name, which can optionally be qualified by a schema name.

simpleColumnName

A simple column name.

You cannot use the same column name more than once in a single <span class="CodeFont">CREATE INDEX</span> statement. Note, however, that a single column name can be used in multiple indexes.

Usage

Splice Machine can use indexes to improve the performance of data manipulation statements. In addition, <span class="CodeFont">UNIQUE</span> indexes provide a form of data integrity checking.

<span class="BoldFont">Index names are unique within a schema</span>. (Some database systems allow different tables in a single schema to have indexes of the same name, but Splice Machine does not.) Both index and table are assumed to be in the same schema if a schema name is specified for one of the names, but not the other. If schema names are specified for both index and table, an exception will be thrown if the schema names are not the same. If no schema name is specified for either table or index, the current schema is used.

By default, Splice Machine uses the ascending order of each column to create the index. Specifying ASC after the column name does not alter the default behavior. <span>The <span class="CodeFont">DESC</span> keyword after the column name causes Splice Machine to use descending order for the column to create the index. Using the descending order for a column can help improve the performance of queries that require the results in mixed sort order or descending order and for queries that select the minimum or maximum value of an indexed column.</span>

If a qualified index name is specified, the schema name cannot begin with SYS.

Indexes and constraints

Unique and primary key constraints generate indexes that enforce or "back" the constraint (and are thus sometimes called <span class="ItalicFont">backing indexes</span>). If a column or set of columns has a <span class="CodeFont">UNIQUE</span> or <span class="CodeFont">PRIMARY KEY</span> constraint on it, you can not create an index on those columns.

Splice Machine has already created it for you with a system-generated name. System-generated names for indexes that back up constraints are easy to find by querying the system tables if you name your constraint. Adding a <span class="CodeFont">PRIMARY KEY</span> or <span class="CodeFont">UNIQUE</span> constraint when an existing <span class="CodeFont">UNIQUE</span> index exists on the same set of columns will result in two physical indexes on the table for the same set of columns. One index is the original <span class="CodeFont">UNIQUE</span> index and one is the backing index for the new constraint.

Statement Dependency System

Prepared statements that involve <span class="CodeFont">SELECT, INSERT, UPDATE</span>, and <span class="CodeFont">DELETE</span> on the table referenced by the <span class="CodeFont">CREATE INDEX</span> statement are invalidated when the index is created.

Example

``` Example
splice> CREATE TABLE myTable (ID INT NOT NULL, NAME VARCHAR(32) NOT NULL );
0 rows inserted/updated/deleted

splice> CREATE INDEX myIdx ON myTable(ID);
0 rows inserted/updated/deleted
```

See Also

-   [<span class="CodeFont">DELETE</span>](Delete.html) statement
-   [<span class="CodeFont">DROP INDEX</span>](DropIndex.html) statement
-   [<span class="CodeFont">INSERT</span>](Insert.html) statement
-   [<span class="CodeFont">SELECT</span>](Select.html) statement
-   [<span class="CodeFont">UPDATE</span>](UpdateTable.html) statement

 


