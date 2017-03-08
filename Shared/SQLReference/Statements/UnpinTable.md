[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/UnpinTable.html)

<a href="" id="Statements.DropTable"></a>[]()UNPIN TABLE
========================================================

The <span class="CodeFont">UNPIN TABLE</span> statement unpins a table, which means that the pinned (previously cached) version of the table no longer exists.

Syntax

``` FcnSyntax
UNPIN TABLE table-Name
```

table-Name

The name of the pinned table that you want to unpin.

Example

``` Example
splice> CREATE TABLE myTbl (col1 int, col2 varchar(10));
0 rows inserted/updated/deleted
splice> INSERT INTO myTbl VALUES (1, 'One'), (2, 'Two');
2 rows inserted/updated/deleted
COL 1      |COL2
---------------------
1           One
2           Two

2 rows selected
splice> PIN TABLE myTbl;
0 rows inserted/updated/deleted
splice> SELECT * FROM myTbl --splice-properties pin=true
> ;
COL 1      |COL2
---------------------
1           One
2           Two

2 rows selected
splice> UNPIN TABLE myTbl;
splice> SELECT * FROM myTbl;
COL 1      |COL2
---------------------
1           One
2           Two

2 rows selected
splice> SELECT * FROM myTbl --splice-properties pin=true
> ERROR: Pinned table read failed with exception 'Table or view not found in database'
```

See Also

-   <span class="CodeFont">[CREATE EXTERNAL TABLE](CreateExternalTable.html)</span> statement
-   <span class="CodeFont">[CREATE TABLE](CreateTable.html)</span> statement
-   <span class="CodeFont">[PIN TABLE](PinTable.html)</span> statement
-   [Query Optimizations](../../Developers/TuningAndDebugging/QueryOptimization.html) in the <span class="ItalicFont">Splice Machine Developer's Guide</span>

 


