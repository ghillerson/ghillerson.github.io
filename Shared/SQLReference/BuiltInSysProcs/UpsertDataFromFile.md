[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/UpsertDataFromFile.html)

<a href="" id="BuiltInSysProcs.ImportData"></a>[]()SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE
=======================================================================================

The SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE system procedure updates or inserts data from a file to a subset of columns in a table. You choose the subset of columns by specifying insert columns.

The syntax and usage of this procedure is almost identical to the syntax and usage of the <span class="CodeFont">[SYSCS\_UTIL.IMPORT\_DATA](ImportData.html)</span> system procedure, except that <span class="CodeFont">SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE</span> first determines if the database already contains a record that matches an incoming record:

-   If a matching record is found in the database, that record is updated with column values from the incoming record.
-   If no matching record is found in the database, the incoming record is added to the database as a new record, exactly as it would be if had you called <span class="CodeFont">[SYSCS\_UTIL.IMPORT\_DATA](ImportData.html)</span>.

After a successful import completes, a simple report displays, showing how many files were imported, and how many record imports succeeded or failed. (Note that you can ignore the <span class="CodeFont">numtasks</span> value shown in this report).

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>On a cluster, the files to be imported <span class="BoldFont">MUST be on HDFS (or MapR-FS)</span>, as must the <span class="CodeFont">badRecordDirectory</span> directory.
In addition, the files must be readable by the <span class="CodeFont">hbase</span> user, and the <span class="CodeFont">badRecordDirectory</span> directory must be writable by the hbase user, either by setting the user explicity, or by opening up the permissions; for example:
        <span class="ShellCommand">sudo -su hdfs hadoop fs -chmod 777 /badRecordDirectory</span>

Syntax

``` FcnSyntax
call SYSCS_UTIL.UPSERT_DATA_FROM_FILE (
               schemaName,
               tableName,
               insertColumnList | null,
               fileOrDirectoryName,
               columnDelimiter | null,
               characterDelimiter | null,
               timestampFormat | null,
               dateFormat | null,
               timeFormat | null,
               badRecordsAllowed,
               badRecordDirectory | null,
               oneLineRecords | null,
               charset | null
);
```

schemaName

The name of the schema of the table in which to import.

tableName

The name of the table in which to import.

insertColumnList

The names, in single quotes, of the columns to import. If this is <span class="CodeFont">null</span>, all columns are imported.

If you don't specify a specify an <span class="CodeFont">insertColumnList</span> and your input file contains more columns than are in the table, then the the extra columns at the end of each line in the input file <span class="BoldFont">are ignored</span>. For example, if your table contains columns <span class="CodeFont">(a, b, c)</span> and your file contains columns <span class="CodeFont">(a, b, c, d, e)</span>, then the data in your file's <span class="CodeFont">d</span> and <span class="CodeFont">e</span> columns will be ignored.

If you do specify an <span class="CodeFont">insertColumnList</span>, and the number of columns doesn't match your table, then any other columns in your table will be replaced by the default value for the table column (or <span class="CodeFont">NULL</span> if there is no default for the column). For example, if your table contains columns <span class="CodeFont">(a, b, c)</span> and you only want to import columns <span class="CodeFont">(a, c)</span>, then the data in table's <span class="CodeFont">b</span> column will be replaced with the default value for that column.

fileOrDirectoryName

Either a single file or a directory. If this is a single file, that file is imported; if this is a directory, all of the files in that directory are imported. Note that files can be compressed or uncompressed, including BZIP2 compressed files.

Note that importing multiple files at once improves parallelism, and thus speeds up the import process. Uncompressed files can be imported faster than compressed files. When using compressed files, the compression algorithm makes a difference; for example,

-   <span class="CodeFont">gzip</span>-compressed files cannot be split during importation, which means that import work on such files cannot be performed in parallel.
-   In contrast, <span class="CodeFont">bzip2</span>-compressed files can be split and thus can be imported using parallel tasks. Note that <span class="CodeFont">bzip2</span> is CPU intensive compared to <span class="CodeFont">LZ4</span> or <span class="CodeFont">LZ0</span>, but is faster than gzip because files can be split.

columnDelimiter

The character used to separate columns, Specify <span class="CodeFont">null</span> if using the comma (<span class="CodeFont">,</span>) character as your delimiter.

In addition to using single characters, you can specify the following special characters as delimiters:

| Special character | Display                                                                                                                                                                                                                                                                                     |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \\t               | Tab                                                                                                                                                                                                                                                                                         |
| \\f               | Formfeed                                                                                                                                                                                                                                                                                    |
| \\b               | Backspace                                                                                                                                                                                                                                                                                   |
| \\\\              | Backslash                                                                                                                                                                                                                                                                                   |
| ^a (or ^A)        | Control-a                                                                                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                  
                     <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you are using a script file from the <span class="CodeFont">splice&gt;</span> command line, your script can contain the actual <span class="CodeFont">Control-a</span> character as the value of this parameter.  |

characterDelimiter

Specifies which character is used to delimit strings in the imported data. You can specify <span class="CodeFont">null</span> or the empty string to use the default string delimiter, which is the double-quote (<span class="CodeFont">"</span>).

In addition to using single characters, you can specify the following special characters as delimiters:

| Special character | Display                                                                                                                                                                                                                                                                                     |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \\t               | Tab                                                                                                                                                                                                                                                                                         |
| \\f               | Formfeed                                                                                                                                                                                                                                                                                    |
| \\b               | Backspace                                                                                                                                                                                                                                                                                   |
| \\\\              | Backslash                                                                                                                                                                                                                                                                                   |
| ^a (or ^A)        | Control-a                                                                                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                  
                     <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you are using a script file from the <span class="CodeFont">splice&gt;</span> command line, your script can contain the actual <span class="CodeFont">Control-a</span> character as the value of this parameter.  |

If your input contains control characters such as newline characters, make sure that those characters are embedded within delimited strings.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>To use the single quote (<span class="CodeFont">'</span>) character as your string delimiter, you need to escape that character. This means that you specify four quotes (<span class="CodeFont">''''</span>) as the value of this parameter. This is standard SQL syntax.
The <a href="#Examples" class="WithinBook MCXref xref xrefWithinBook">Examples</a> section below contains an example that uses the single quote as the string delimiter character.

timestampFormat

The format of timestamps stored in the file. You can set this to <span class="CodeFont">null</span> if there are no time columns in the file, or if the format of any timestamps in the file match the <span class="CodeFont">Java.sql.Timestamp</span> default format, which is: "<span class="ItalicFont">yyyy-MM-dd HH:mm:ss</span>". See the <a href="#TimestampFormats" class="WithinBook MCXref xref xrefWithinBook">About Timestamp Formats</a> section below for more information about timestamps.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>All of the timestamps in the file you are importing must use the same format.

dateFormat

The format of datestamps stored in the file. You can set this to <span class="CodeFont">null</span> if there are no date columns in the file, or if the format of any dates in the file match pattern: "<span class="ItalicFont">yyyy-MM-dd</span>".

timeFormat

The format of time values stored in the file. You can set this to null if there are no time columns in the file, or if the format of any times in the file match pattern: "<span class="ItalicFont">HH:mm:ss</span>".

badRecordsAllowed

The number of rejected (bad) records that are tolerated before the import fails. If this count of rejected records is reached, the import fails, and any successful record imports are rolled back.

-   If you specify <span class="CodeFont">-1</span> as the value of this parameter, all record import failures are tolerated and logged.
-   If you specify <span class="CodeFont">0</span> as the value of this parameter, the import will fail if even one record is bad.

In previous releases of Splice Machine, this parameter was named <span class="CodeFont">failBadRecordCount</span>, and a value of <span class="CodeFont">0</span> meant that all record import failures were tolerated. This has been changed, and you now must specify a value of <span class="CodeFont">-1</span> for <span class="CodeFont">badRecordsAllowed</span> to tolerate all bad records.

badRecordDirectory

The directory in which bad record information is logged. Splice Machine logs information to the <span class="CodeFont"><span class="CodeItalicFont">&lt;import\_file\_name&gt;</span>.bad</span> file in this directory; for example, bad records in an input file named <span class="CodeFont">foo.csv</span> would be logged to a file named <span class="ItalicFont">badRecordDirectory</span><span class="CodeFont">/foo.csv.bad</span>.

The default value is the directory in which the import files are found.

oneLineRecords

A Boolean value that specifies whether each line in the import file contains one complete record:

-   If you specify <span class="CodeFont">true</span> or <span class="CodeFont">null</span>, then each record is expected to be found on a single line in the file.
-   If you specify <span class="CodeFont">false</span>, records can span multiple lines in the file.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Multi-line record files are slower to load, because the file cannot be split and processed in parallel; if you import a directory of multiple line files, each file as a whole is processed in parallel, but no splitting takes place.

charset

The character encoding of the import file. The default value is UTF-8. Currently, any other value is ignored and UTF-8 is used.

Results

<span class="CodeFont">SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE</span> displays a summary of the import process results that looks like this:

``` Example
rowsImported   |failedRows   |files   |dataSize   |failedLog
-------------------------------------------------------------
94             |0            |1       |4720       |NONE
```

This procedure also logs rejected record activity into <span class="CodeFont">.bad</span> files in the <span class="CodeFont">badRecordDirectory</span> directory; one file for each imported file.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>After importing a large amount of data into a table, it is useful to run a full compaction on table; see the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_TABLE](PerformMajorCompactionOnTable.html)</span> system procedure.

### Importing a Subset of Data From a File

When you import data from a file into a table, all of the data in the file is not necessarily imported. This can happen in either of these circumstances:

-   If the table into which you're importing contains less columns than does the data file, the "extra" columns of data are ignored.
-   If the <span class="CodeFont">insertColumnList</span> in your import call specifies only a subset of the columns in the data file.

You can find examples in the [Importing Data Into Splice Machine](../../Developers/ImportingData.html) topic in our <span class="ItalicFont">Administrator's Guide</span>.

Note that you can take advantage of this by importing different subsets of data from one input file into multiple tables in your database.

Usage

This procedure will only work correctly if the table into which you are inserting/updating data has primary keys.

When you generate the input file, it must:

-   contain the columns to be changed
-   contain all <span class="CodeFont">NON\_NULL</span> columns

Record Import Failure Reasons
-----------------------------

When upserting data from a file, the input file you generate must contain:

-   the columns to be changed
-   all <span class="CodeFont">NON\_NULL</span> columns

Typical reasons for a row (record) import to fail include:

-   Improper data expected for a column.
-   Improper number of columns of data.
-   A primary key violation: [<span class="CodeFont">SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE</span>](#) will only work correctly if the table into which you are inserting/updating has primary keys.

Handling Generated Column Values in Imported Files
--------------------------------------------------

If you're importing data into a table with generated columns (see <span class="CodeFont"><a href="../Statements/GeneratedColumnSpec.html" class="MCXref xref">generated-column-spec</a></span> in the <span class="ItalicFont">SQL Reference Manual</span>), you should know that imported records are handled in exactly the same manner as are records inserted using the <span class="CodeFont"><a href="../Statements/Insert.html" class="MCXref xref">INSERT</a></span> statement.

Here's a simple summary of what happens for generated columns, including <span class="CodeFont">DEFAULT</span> values, in imported records:

-   If your <span class="CodeFont">importColumnList</span> includes the column name and the imported column value is empty, <span class="CodeFont">NULL</span> is inserted into the database table column.
-   If your <span class="CodeFont">importColumnList</span> includes the column name and the imported column value is not empty, the column value is imported unless the value is not valid in the table.
-   If you <span class="CodeFont">importColumnList</span> does not include the column name, the generated value is inserted into the database table column.

### Generated Column Import Examples

To illustrate what happens with generated column values in imported records, we'll use this simple database table created with this statement:

``` Example
CREATE TABLE myTable (
   colA INT,
   colB CHAR(4) DEFAULT 'myDefaultVal',
   colC INT);
```

| <span class="CodeBoldFont">insertColumnList</span> | Values in import record | Values inserted into database | Notes                                                                |
|----------------------------------------------------|-------------------------|-------------------------------|----------------------------------------------------------------------|
| "A,B,C"                                            | 1,,2                    | \[1,NULL,2\]                  |                                                                      |
| "A,B,C"                                            | 3,de,4                  | \[3,de,4\]                    |                                                                      |
| "A,B,C"                                            | 1,2                     | Error: column B wrong type    |                                                                      |
| "A,B,C"                                            | 1,DEFAULT,2             | \[1,"DEFAULT",2\]             | <span class="CodeFont">DEFAULT</span> is imported as a literal value |
| Empty                                              | 1,,2                    | \[1,NULL,2\]                  |                                                                      |
| Empty                                              | 3,de,4                  | \[3,de,4\]                    |                                                                      |
| Empty                                              | 1,2                     | Error: column B wrong type    |                                                                      |
| "A,C"                                              | 1,2                     | \[1,myDefaultVal,2\]          |                                                                      |
| "A,C"                                              | 3,4                     | \[3,myDefaultVal,4\]          |                                                                      |

Note that the value <span class="CodeFont">DEFAULT</span> in the imported file <span class="BoldFont">is not interpreted</span> to mean that the default value should be applied to that column; instead:

-   If the target column in your database has a string data type, such as <span class="CodeFont">CHAR</span> or <span class="CodeFont">VARCHAR</span>, the literal value <span class="CodeFont">"DEFAULT"</span> is inserted into your database..
-   If the target column is not a string data type, an error will occur.

### How to Use Generated Values for a Column in Some (but not all) Imported Records

If you are importing a file into a table with a generated column, and you want to import some records with actual values and apply generated values to other records, you need to split your import file into two files and import each:

-   Import the file containing records with non-default values with the column name included in the <span class="CodeFont">insertColumnList</span>.
-   Import the file containing records with default values with the column name excluded from the <span class="CodeFont">insertColumnList</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>When you export a table with generated columns to a file, the actual column values are exported, so importing that same file into a different database will accurately replicate the original table values.

[]()About Timestamp Formats
---------------------------

Splice Machine uses the following Java date and time pattern letters to construct timestamps:

| Pattern Letter | Description            | Format(s)                                                                                                                                                                              |
|----------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| y              | year                   | yy or yyyy                                                                                                                                                                             |
| M              | month                  | MM                                                                                                                                                                                     |
| d              | day in month           | dd                                                                                                                                                                                     |
| h              | hour (0-12)            | hh                                                                                                                                                                                     |
| H              | hour (0-23)            | HH                                                                                                                                                                                     |
| m              | minute in hour         | mm                                                                                                                                                                                     |
| s              | seconds                | ss                                                                                                                                                                                     |
| S              | tenths of seconds      | S, SS, SSS, SSSS, SSSSS or SSSSSS<span class="important">\*</span>                                                                                                                     
                                                                                                                                                                                                                                   
                                           <span class="important">\*</span><span class="bodyFont">Specify </span>SSSSSS <span class="bodyFont">to allow a variable number (any number) of digits after the decimal point.</span>  |
| z              | time zone text         | e.g. Pacific Standard time                                                                                                                                                             |
| Z              | time zone, time offset | e.g. -0800                                                                                                                                                                             |

The default timestamp format for Splice Machine imports is: <span class="CodeFont">yyyy-MM-dd HH:mm:ss</span>, which uses a 24-hour clock, does not allow for decimal digits of seconds, and does not allow for time zone specification.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The standard Java library does not support microsecond precision, so you <span class="BoldFont">cannot</span> specify millisecond (<span class="CodeFont">S</span>) values in a custom timestamp format and import such values with the desired precision.

### Timestamps and Importing Data at Different Locations

Note that timestamp values are relative to the geographic location at which they are imported, or more specifically, relative to the timezone setting and daylight saving time status where the data is imported.

This means that timestamp values from the same data file may appear differently after being imported in different timezones.

### Examples

The following tables shows valid examples of timestamps and their corresponding format (parsing) patterns:

| Timestamp value             | Format Pattern           | Notes                                                                                                |
|-----------------------------|--------------------------|------------------------------------------------------------------------------------------------------|
| 2013-03-23 09:45:00         | yyyy-MM-dd HH:mm:ss      | This is the default pattern.                                                                         |
| 2013-03-23 19:45:00.98-05   | yyyy-MM-dd HH:mm:ss.SSZ  | This pattern allows up to 2 decimal digits of seconds, and requires a time zone specification.       |
| 2013-03-23 09:45:00-07      | yyyy-MM-dd HH:mm:ssZ     | This patterns requires a time zone specification, but does not allow for decimal digits of seconds.  |
| 2013-03-23 19:45:00.98-0530 | yyyy-MM-dd HH:mm:ss.SSZ  | This pattern allows up to 2 decimal digits of seconds, and requires a time zone specification.       |
| 2013-03-23 19:45:00.123     
                              
 2013-03-23 19:45:00.12       | yyyy-MM-dd HH:mm:ss.SSS  | This pattern allows up to 3 decimal digits of seconds, but does not allow a time zone specification. 
                                                                                                                                                                
                                                          Note that if your data specifies more than 3 decimal digits of seconds, an error occurs.              |
| 2013-03-23 19:45:00.1298    | yyyy-MM-dd HH:mm:ss.SSSS | This pattern allows up to 4 decimal digits of seconds, but does not allow a time zone specification. |

Please see <span class="ItalicFont">[Working With Date and Time Values](../../Developers/Fundamentals/WorkingWithDates.html)</span> in the <span class="ItalicFont">Developer's Guide</span> for information working with timestamps, dates, and times.

[]()Examples

The examples in this section illustrate using different timestamp formats and different string delimiter characters.

Example 1: Specifying a timestamp format for an entire table

Use a single timestamp format for the entire table by explicitly specifying a single <span class="CodeFont">timeStampFormat</span>.

``` Example
Mike,2013-04-21 09:21:24.98-05
Mike,2013-04-21 09:15:32.78-04
Mike,2013-03-23 09:45:00.68-05
```

You can then import the data with the following call:

``` Example
call SYSCS_UTIL.UPSERT_DATA_FROM_FILE('app','tabx','c1,c2',
    '/path/to/ts3.csv',
    ',', '''', 
    'yyyy-MM-dd HH:mm:ss.SSZ',
    null, null, 0, null, true, null);
```

Note that for any import use case shown above, the time shown in the imported table depends on the timezone setting where the data is imported. In other words, given the same csv file, if imported at locations with different time zones, the value in the table shown will be different. Additionally, daylight savings time may account for a 1-hour difference if timezone is specified.

Example 2: Importing strings with embedded special characters

This example imports a csv file that includes newline (<span class="CodeFont">Ctrl-M</span>) characters in some of the input strings. We use the default double-quote as our character delimiter to import data such as the following:

``` Example
1,This field is one line,Able
2,"This field has two lines
This is the second line of the field",Baker
3,This field is also just one line,Charlie
```

We then use the following call to import the data:

``` Example
SYSCS_UTIL.UPSERT_DATA_FROM_FILE('SPLICE','MYTABLE',null,'data.csv','\t',null,null,null,null,0,'BAD', false, null);
```

We can also explicitly specify double quotes (or any other character) as our delimiter character for strings:

``` Example
SYSCS_UTIL.UPSERT_DATA_FROM_FILE('SPLICE','MYTABLE',null,'data.csv','\t','"',null,null,null,0,'BAD', false, null);
```

Example 3: Using single quotes to delimit strings

This example performs the same import as the previous example, simply substituting single quotes for double quotes as the character delimiter in the input:

``` Example
1,This field is one line,Able
2,'This field has two lines
This is the second line of the field',Baker
3,This field is also just one line,Charlie
```

Note that you must escape single quotes in SQL, which means that you actually define the character delimiter parameter with four single quotes, as follow

``` Example
SYSCS_UTIL.UPSERT_DATA_FROM_FILE('SPLICE','MYTABLE',null,'data.csv','\t','''',null,null,null,0,'BAD', false, null);
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.IMPORT\_DATA</span>](ImportData.html)

 


