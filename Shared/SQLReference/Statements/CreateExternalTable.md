[Open topic with navigation](../../../index.html#Shared/SQLReference/Statements/CreateExternalTable.html)

<a href="" id="Statements.CreateTable"></a>[]()CREATE EXTERNAL TABLE
====================================================================

A <span class="CodeFont">CREATE EXTERNAL TABLE</span> statement creates a table in Splice Machine that you can use to query data that is stored externally in a flat file, such as a file in Parquet, ORC, or plain text format. External tables are largely used as a convenient means of moving data into and out of your database.

You can query external tables just as you would a regular Splice Machine table; however, you cannot perform any DML operations on an external table, once it has been created. That also means that you cannot create an index on an external table.

<span class="autonumber"><span class="noteAutoNum">IMPORTANT:  </span></span>If the schema of the external file that you are querying is modified outside of Splice, you need to manually refresh the Splice Machine table by calling the <span class="CodeFont">[REFRESH EXTERNAL TABLE](../BuiltInSysProcs/RefreshExternalTable.html)</span> built-in system procedure.

If a qualified table name is specified, the schema name cannot begin with <span class="CodeFont">SYS</span>.

Syntax

``` FcnSyntax
CREATE EXTERNAL TABLE table-Name
  {
    ( column-definition[, column-definition]* )
    [ COMPRESSED WITH compression-format ]
    [ PARTITIONED BY (column-name ) ]}
    [ ROW FORMAT DELIMITED
       [ FIELDS TERMINATED BY char [ESCAPED BY char] ]
       [ LINES TERMINATED BY char ]
    ]
    STORED AS file-format LOCATION location
  }
```

table-Name

The name to assign to the new table.

compression-format

The compression algorithm used to compress the flat file source of this external table. You can specify one of the following values:

-   <span class="CodeFont">ZLIB</span>
-   <span class="CodeFont">SNAPPY</span>

If you don't specify a compression format, the default is uncompressed. You cannot specify a <span class="CodeItalicFont">compression-format</span> when using the <span class="CodeFont">TEXTFILE </span><span class="CodeItalicFont">file-format</span>; doing so generates an error.

column-definition

A column definition.

The maximum number of columns allowed in a table is <span class="CodeFont"><span class="LimitationsMaxColumnsInTable">100000</span></span>.

column-name

The name of a column.

char

A single character used as a delimiter or escape character. Enclose this character in single quotes; for example, ','.

To specify a special character that includes the backslash character, you must escape the backslash character itself. For example:

-   <span class="CodeFont">\\\\</span> to indicate a backslash character
-   <span class="CodeFont">\\n</span> to indicate a newline character
-   <span class="CodeFont">\\t</span> to indicate a tab character

file-format

The format of the flat file source of this external table. This is currently one of these values:

-   <span class="CodeFont">ORC</span> is a columnar storage format
-   <span class="CodeFont">PARQUET</span> is a columnar storage format
-   <span class="CodeFont">TEXTFILE</span> is a plain text file

location

The location at which the file is stored.

Usage Notes

Here are some notes about using external tables:

-   If the data types in the table schema you specify do not match the schema of the external file, an error occurs and the table is not created.
-   You cannot define indexes or constraints on external tables
-   The <span class="CodeFont">ROW FORMAT</span> parameter is not supported for columnar storage format files (<span class="CodeFont">ORC</span> or <span class="CodeFont">PARQUET</span> files).
-   If you specify the location of a non-existent file when you create an external table, Splice Machine automatically creates an external file at that location.
-   Splice Machine isn't able to know when the schema of the file represented by an external table is updated; when this occurs, you need to update the external table in Splice Machine by calling the [SYSCS\_UTIL.SYSCS\_REFRESH\_EXTERNAL\_TABLE](../BuiltInSysProcs/RefreshExternalTable.html) built-in system procedure.
-   You cannot specify a <span class="CodeItalicFont">compression-format</span> when using the <span class="CodeFont">TEXTFILE </span><span class="CodeItalicFont">file-format</span>; doing so generates an error.

Examples

This section presents examples of the <span class="CodeFont">CREATE EXTERNAL TABLE</span> statement.

This example creates an external table for a <span class="CodeFont">PARQUET</span> file:

``` Example
splice> CREATE EXTERNAL TABLE myParquetTable(
      col1 INT, col2 VARCHAR(24))
   PARTITIONED BY (col1)
   STORED AS PARQUET
   LOCATION '/users/myName/myParquetFile';
0 rows inserted/updated/deleted
```

This example creates an external table for an <span class="CodeFont">ORC</span> file and inserts data into it:

``` Example
splice> CREATE EXTERNAL TABLE myOrcTable(
   col1 INT, col2 VARCHAR(24))
   PARTITIONED BY (col1)
   STORED AS ORC
   LOCATION '/users/myName/myOrcFile';
0 rows inserted/updated/deleted

splice> INSERT INTO myOrcTable VALUES (1, 'One'), (2, 'Two'), (3, 'Three');
3 rows inserted/updated/deleted

splice> SELECT * FROM myOrcTable;
COL1        |COL2
------------------------------------
3           |Three
2           |Two
1           |One
```

This example creates an external table for a plain text file:

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

This example creates an external table for a <span class="CodeFont">PARQUET</span> file that was compressed with Snappy compression:

``` Example
splice> CREATE EXTERNAL TABLE mySnappyParquetTable(
      col1 INT, col2 VARCHAR(24))
   PARTITIONED BY (col1)
   STORED AS PARQUET
   LOCATION '/users/myName/mySnappyParquetFile'
   COMPRESSED WITH SNAPPY;
0 rows inserted/updated/deleted
```

See Also

-   <span class="CodeFont">[CREATE TABLE](CreateTable.html)</span> statement
-   <span class="CodeFont">[PIN TABLE](PinTable.html)</span> statement
-   <span class="CodeFont">[DROP TABLE](DropTable.html)</span> statement
-   <span class="CodeFont">[REFRESH EXTERNAL TABLE](../BuiltInSysProcs/RefreshExternalTable.html)</span> built-in system procedure
-   [Foreign Keys](../../Developers/Fundamentals/ForeignKeys.html) in the <span class="ItalicFont">Developer's Guide</span>.
-   [Triggers](../../Developers/Fundamentals/DatabaseTriggers.html) in the <span class="ItalicFont">Developer's Guide</span>.

 


