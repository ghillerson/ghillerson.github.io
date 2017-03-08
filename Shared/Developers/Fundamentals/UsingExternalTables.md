[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/UsingExternalTables.html)

Using the Splice Machine External Table Feature
===============================================

This topic covers the use of external tables in Splice Machine. An external table references a file stored in a flat file format. You can use flat files that are stored in one of these formats:

-   <span class="CodeFont">ORC</span> is a columnar storage format
-   <span class="CodeFont">PARQUET</span> is a columnar storage format
-   <span class="CodeFont">TEXTFILE</span> is a plain text file

You can access <span class="CodeFont">ORC</span> and <span class="CodeFont">PARQUET</span> files that have been compressed with either Snappy or ZLIb compression; however, you cannot use a compressed plain text file.

About External Tables
---------------------

You can use Splice Machine external tables to query the contents of flat files that are stored outside of your database. You query external tables pretty much the same way as you do the tables in your database.

External tables reference files that are stored in a flat file format such as Apache Parquet or Apache Orc, both of which are columnar storage formats that are available in Hadoop. You can use the <span class="CodeFont">[CREATE EXTERNAL TABLE](../../SQLReference/Statements/CreateExternalTable.html)</span> statement to create an external table that is connected to a specific flat file.

Using External Tables
---------------------

This section presents several examples of using external tables with Splice Machine.

Accessing a Parquet File

The following statement creates an external table for querying a <span class="CodeFont">PARQUET</span> file that is stored on your computer:

``` Example
splice> CREATE EXTERNAL TABLE myExtTbl (
      col1 INT, col2 VARCHAR(24))
   PARTITIONED BY (col1)
   STORED AS PARQUET
   LOCATION '/users/myname/myParquetFile';
0 rows inserted/updated/deleted
```

The call to <span class="CodeFont">CREATE EXTERNAL TABLE</span> associates a Splice Machine external table with the file named <span class="CodeFont">myparquetfile</span>, and tells Splice Machine that:

-   The table should be partitioned based on the values in <span class="CodeFont">col1</span>.
-   The file is stored in PARQUET format.
-   The file is located in <span class="CodeFont">/users/myname/myParquetFile</span>.

After you create the external table, you can query <span class="CodeFont">myExtTbl</span> just as you would any other table in your database.

Accessing and Updating an ORC File

The following statement creates an external table for creates an external table for an <span class="CodeFont">ORC</span> file and inserts data into it:

``` Example
splice> CREATE EXTERNAL TABLE myExtTbl2(
   col1 INT, col2 VARCHAR(24))
   PARTITIONED BY (col1)
   STORED AS ORC
   LOCATION '/users/myname/myOrcFile';
0 rows inserted/updated/deleted

splice> INSERT INTO myExtTbl2 VALUES (1, 'One'), (2, 'Two'), (3, 'Three');
3 rows inserted/updated/deleted

splice> SELECT * FROM myExtTbl2;
COL1        |COL2
------------------------------------
3           |Three
2           |Two
1           |One
```

The call to <span class="CodeFont">CREATE EXTERNAL TABLE</span> associates a Splice Machine external table with the file named <span class="CodeFont">myOrcFile</span>, and tells Splice Machine that:

-   The table should be partitioned based on the values in <span class="CodeFont">col1</span>.
-   The file is stored in ORC format.
-   The file is located in <span class="CodeFont">/users/myname/myOrcFile</span>.

The call to <span class="CodeFont">INSERT INTO </span> demonstrates that you can insert values into the external table just as you would with an ordinary table.

Accessing a Plain Text File

You can specify a table constraint on an external table; for example:

``` Example
splice> CREATE EXTERNAL TABLE myTextTable(
   col1 INT, col2 VARCHAR(24))
   PARTITIONED BY (col1)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' ESCAPED BY '\\'
   LINES TERMINATED BY '\\n'
   STORED AS TEXTFILE
   LOCATION '/users/myName/myTextFile';
0 rows inserted/updated/deleted
```

The call to <span class="CodeFont">CREATE EXTERNAL TABLE</span> associates a Splice Machine external table with the file named <span class="CodeFont">myOrcFile</span>, and tells Splice Machine that:

-   The table should be partitioned based on the values in <span class="CodeFont">col1</span>.
-   Each field in each row is terminated by a comma.
-   Each line in the file is terminated by a line-end character.
-   The file is stored in plain text format.
-   The file is located in <span class="CodeFont">/users/myName/myTextFile</span>.

Accessing a Compressed File

This example is exactly the same as our first example, except that the source file has been compressed with Snappy compression:

``` Example
splice> CREATE EXTERNAL TABLE myExtTbl (
      col1 INT, col2 VARCHAR(24))
   COMPRESSED WITH SNAPPY
   PARTITIONED BY (col1)
   STORED AS PARQUET
   LOCATION '/users/myname/myParquetFile';
0 rows inserted/updated/deleted
```

Manually Refreshing an External Tables
--------------------------------------

If the schema of the file represented by an external table is updated, Splice Machine needs to refresh its representation. When you use the external table, Spark caches its schema in memory to improve performance; as long as you are using Spark to modify the table, it is smart enough to refresh the cached schema. However, if the table schema is modified outside of Spark, you need to call the [SYSCS\_UTIL.SYSCS\_REFRESH\_EXTERNAL\_TABLE](../../SQLReference/BuiltInSysProcs/RefreshExternalTable.html) built-in system procedure. For example:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_REFRESH_EXTERNAL_TABLE('APP', 'myExtTable');
Statement executed.
```

See Also

The <span class="CodeFont">[CREATE EXTERNAL TABLE](../../SQLReference/Statements/CreateExternalTable.html)</span> statement.

The <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_REFRESH\_EXTERNAL\_TABLE](../../SQLReference/BuiltInSysProcs/RefreshExternalTable.html)</span> built-in system procedure.

 


