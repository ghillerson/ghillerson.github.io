[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/PinTable.html)

[]()PIN TABLE
=============

The <span class="CodeFont">PIN TABLE</span> statement allows you to pin (cache) a table in memory, which can improve performance for tables that are being used frequently in analytic operations.

<span class="autonumber"><span class="noteAutoNum">IMPORTANT:  </span></span>The pinned version of a table is a static version of that table; updates to the underlying table are not automatically reflected in the pinned version. To refresh the pinned version, you need to unpin and then repin the table, as described in the [Usage Notes](#Usage) section below.

Syntax

``` FcnSyntax
PIN TABLE tableName;
```

tableName

A string that specifies the name of the table that you want to pin in memory.

An error occurs if the named table does not exist.

[]()Usage Notes

Here are a few important notes about using pinned tables:

-   <a href="#Pinned" class="MCXref xref">Pinned and Unpinned Table Versions</a>
-   <a href="#Refreshi" class="MCXref xref">Refreshing the Pinned Version of a Table</a>
-   <a href="#Unpinnin" class="MCXref xref">Unpinning and Dropping Pinned Tables</a>

[]()Pinned and Unpinned Table Versions

Once you pin a table, you effectively have two versions of it to work with:

-   The original table continues to work just as usual
-   The pinned version is a static version of the table at the time you pinned it. To access the pinned version of a table, you must specify the Splice <span class="CodeFont">pin=true</span> property. If you do not specify this property in your query, the query will operate on the unpinned version of the table.

The pinned version (version) of a table is statically cached in memory; this means that:

-   Updates to the table (unpinned version) are not automatically reflected in the pinned version of the table.
-   Updates to the pinned version of the table are not permitted: you cannot insert into, delete from, or update the pinned version of a table.

Here's a simple example that illustrates these qualities:

``` Example
splice> CREATE TABLE myTbl (col1 int, col2 varchar(10));
0 rows inserted/updated/deleted
splice> INSERT INTO myTbl VALUES (1, 'One'), (2, 'Two');
2 rows inserted/updated/deleted
splice> PIN TABLE myTbl;
0 rows inserted/updated/deleted
splice> INSERT INTO myTbl VALUES (3, 'Three'), (4, 'Four');
2 rows inserted/updated/deleted
splice> SELECT * FROM myTbl;
COL1      |COL2
---------------------
1           One
2           Two
3           Three
4           Four

4 rows selected
splice> SELECT * FROM myTbl --splice-properties pin=true
> ;
COL1      |COL2
---------------------
1           One
2           Two

2 rows selected
splice> UPDATE myTbl SET col1=11 WHERE col1=1;
1 row inserted/updated/deleted
splice> UPDATE myTbl --splice-properties pin=true
SET col1=21 WHERE col1=2;
ERROR: Pinned Table read failed with exception Table or view not found in database.
```

[]()Refreshing the Pinned Version of a Table

If you update the table and want the pinned version to reflect those updates, you need to refresh your pinned table version. You can simply unpin the table from memory, and then repin it into memory:

``` Example
splice> UNPIN TABLE Players;
0 rows inserted/updated/deleted
splice> PIN TABLE Players;
0 rows inserted/updated/deleted
```

Now the pinned version of the table matches the original version.

[]()Unpinning and Dropping Pinned Tables

When you drop a table (with the <span class="CodeFont">[DROP TABLE](DropTable.html)</span> statement), the pinned version is automatically deleted and can no longer be used.

To delete just the pinned version of a table, use the <span class="CodeFont">[UNPIN TABLE](UnpinTable.html)</span> statement.

See Also

-   <span class="CodeFont">[CREATE EXTERNAL TABLE](CreateExternalTable.html)</span> statement
-   <span class="CodeFont">[CREATE TABLE](CreateTable.html)</span> statement
-   <span class="CodeFont">[UNPIN TABLE](UnpinTable.html)</span> statement
-   [Query Optimizations](../../Developers/TuningAndDebugging/QueryOptimization.html) in the <span class="ItalicFont">Splice Machine Developer's Guide</span>

 


