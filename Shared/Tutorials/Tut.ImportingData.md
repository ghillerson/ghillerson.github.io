[Open topic with navigation](../../index.html#Shared/Tutorials/Tut.ImportingData.html)

Tutorial: Help with Importing Data Into Splice Machine
======================================================

This tutorial will help you to import your data into Splice Machine; the number of options available for importing can make this seem like a more complicated process than it really is. This topic contains the following sections:

-   <a href="#Our" class="MCXref xref">Our Import Procedures</a> is a very brief description of our built-in procedures for importing (bulk-loading) data into your Splice Machine database.
-   <a href="#Tips" class="MCXref xref">Tips for Using Our Import Procedures</a> includes a number of tips that will help you to smoothly navigate your import tasks.
-   <a href="#Examples" class="MCXref xref">Examples</a> contains several simple import examples.

[]()Our Import Procedures
-------------------------

Splice Machine provides two built-in system procedures for importing data: <span class="CodeFont">[SYSCS\_UTIL.IMPORT\_DATA](../SQLReference/BuiltInSysProcs/ImportData.html)</span> and <span class="CodeFont">[SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE](../SQLReference/BuiltInSysProcs/UpsertDataFromFile.html)</span>. These procedures are nearly identical in syntax and function; the difference is that when you upsert into your database, the procedure first determines if the database already contains a record that matches an incoming record:

-   If a matching record is found in the database, that record is updated with column values from the incoming record.
-   If no matching record is found in the database, the incoming record is added to the database as a new record, exactly as it would be if had you called <span class="CodeFont">[SYSCS\_UTIL.IMPORT\_DATA](../SQLReference/BuiltInSysProcs/ImportData.html)</span>.

Both procedures import data to a subset of columns in a table. You choose the subset of columns by specifying insert columns. We apply error and consistency checking of incoming data, and allow you to monitor import progress, using the [<span class="ItalicFont">Splice Machine Management Console Guide</span>](../ManagementConsole/Intro.ManagementConsole.html) to monitor progress

Here's the syntax for both procedures:

``` FcnSyntax
call SYSCS_UTIL.IMPORT_DATA (
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

And here is a summary of the parameters. For more information about these parameters, see the <span class="CodeFont">[SYSCS\_UTIL.IMPORT\_DATA](../SQLReference/BuiltInSysProcs/ImportData.html)</span> and <span class="CodeFont">[SYSCS\_UTIL.UPSERT\_DATA\_FROM\_FILE](../SQLReference/BuiltInSysProcs/UpsertDataFromFile.html)</span> topics in our SQL Reference Manual.

schemaName

The name of the schema of the table in which to import.

tableName

The name of the table in which to import.

insertColumnList

The names, in single quotes, of the columns to import. If this is <span class="CodeFont">null</span>, all columns are imported.

fileOrDirectoryName

Either a single file or a directory. If this is a single file, that file is imported; if this is a directory, all of the files in that directory are imported. Note that files can be compressed or uncompressed, including BZIP2 compressed files.

See [Tip \#1](#Tip) below.

columnDelimiter

The character used to separate columns, Specify <span class="CodeFont">null</span> if using the comma (<span class="CodeFont">,</span>) character as your delimiter.

See [Tip \#4](#Tip4) below.

characterDelimiter

Specifies which character is used to delimit strings in the imported data. You can specify <span class="CodeFont">null</span> or the empty string to use the default string delimiter, which is the double-quote (<span class="CodeFont">"</span>).

If your input contains control characters such as newline characters, make sure that those characters are embedded within delimited strings.

See [Tip \#4](#Tip4) below.

timestampFormat

The format of time values stored in the file. You can set this to <span class="CodeFont">null</span> if there are no timestamp columns in the file, or if the format of any timestamps in the file match the <span class="CodeFont">Java.sql.Timestamp</span> default format, which is: "<span class="ItalicFont">yyyy-MM-dd HH:mm:ss</span>".

See [Tip \#5](#Tip5) below.

dateFormat

The format of dates stored in the file. You can set this to <span class="CodeFont">null</span> if there are no date columns in the file, or if the format of any dates in the file match pattern: "<span class="ItalicFont">yyyy-MM-dd</span>".

See [Tip \#5](#Tip5) below.

timeFormat

The format of timeFormats stored in the file. You can set this to null if there are no time columns in the file, or if the format of any times in the file match pattern: "<span class="ItalicFont">HH:mm:ss</span>".

See [Tip \#5](#Tip5) below.

badRecordsAllowed

The number of rejected (bad) records that are tolerated before the import fails. If this count of rejected records is reached, the import fails, and any successful record imports are rolled back.

-   If you specify <span class="CodeFont">-1</span> as the value of this parameter, all record import failures are tolerated and logged.
-   If you specify <span class="CodeFont">0</span> as the value of this parameter, the import will fail if even one record is bad.

badRecordDirectory

The directory in which bad record information is logged. Splice Machine logs information to the <span class="CodeFont"><span class="CodeItalicFont">&lt;import\_file\_name&gt;</span>.bad</span> file in this directory; for example, bad records in an input file named <span class="CodeFont">foo.csv</span> would be logged to a file named <span class="ItalicFont">badRecordDirectory</span><span class="CodeFont">/foo.csv.bad</span>.

The default value is the directory in which the import files are found.

See [Tip \#6](#Tip6) below.

oneLineRecords

A Boolean value that specifies whether each line in the import file contains one complete record:

-   If you specify <span class="CodeFont">true</span> or <span class="CodeFont">null</span>, then each record is expected to be found on a single line in the file.
-   If you specify <span class="CodeFont">false</span>, records can span multiple lines in the file.

See [Tip \#7](#Tip7) below.

charset

The character encoding of the import file. The default value is UTF-8. Currently, any other value is ignored and UTF-8 is used.

[]()Tips for Using Our Import Procedures
----------------------------------------

This section contains a number of tips that our users have found very useful in determining the parameter settings to use when running an import:

1.  [](#Tip)<a href="#Tip" class="MCXref xref">Tip #1:  Specifying the File Location</a>
2.  [](#Tip2)<a href="#Tip2" class="MCXref xref">Tip #2:  Import Large Datasets in Groups of Files</a>
3.  [](#Tip3)<a href="#Tip3" class="MCXref xref">Tip #3:  Don't Compress Your Files With GZIP</a>
4.  [](#Tip4)<a href="#Tip4" class="MCXref xref">Tip #4:  Use Special Characters for Delimiters</a>
5.  [](#Tip5)<a href="#Tip5" class="MCXref xref">Tip #5:  Avoid Problems With Date, Time, and Timestamp Formats</a>
6.  [](#Tip6)<a href="#Tip6" class="MCXref xref">Tip #6:  Change the Bad Directory for Each Table / Group</a>
7.  [](#Tip7)<a href="#Tip7" class="MCXref xref">Tip #7:  Importing Multi-line Records</a>
8.  [](#Tip8)<a href="#Tip8" class="MCXref xref">Tip #8:  Importing Clobs and Blobs</a>
9.  [](#Tip9)<a href="#Tip9" class="MCXref xref">Tip #9:  Scripting Your Imports</a>

### []()Tip \#1:  Specifying the File Location

Some customers get confused by the the <span class="CodeFont">fileOrDirectoryName</span> parameter. How you use this depends on whether you are importing a single file or a directory of files. It also depends on whether you're running the standalone or cluster version of Splice Machine.

If you are running a stand alone environment, the name or path will be to a file or directory on the file system. For example:

``` Example
/users/myname/mydata/mytable.csv
/users/myname/mydatadir
```

However, if you are running this on a cluster, the path is to a file on HDFS (or the MapR File system). For example:

``` Example
/data/mydata/mytable.csv
/data/myname/mydatadir
```

### []()Tip \#2:  Import Large Datasets in Groups of Files

If you have a lot of data (100s of millions or billions of records), you may be tempted to create one massive file that contains all of your records and import that file; Splice Machine recommends against this; instead, we urge you to manage your data in smaller files. Specifically, we suggest that you split your data into files that are:

-   approximately 40 GB
-   have approximately 50 million records, depending on how wide your table is

If you have a lot of files, group them into multiple directories, and import each directory individually. For example, here is a structure our Customer Success engineers like to use:

-   /data/mytable1/group1
-   /data/mytable1/group2
-   /data/mytable1/group3

### []()Tip \#3:  Don't Compress Your Files With GZIP

We recommend importing files that are either uncompressed, or have been compressed with <span class="CodeBoldFont">bz2</span> or <span class="CodeBoldFont">lz4</span> compression.

If you import files compressed with <span class="CodeFont">gzip</span>, Splice Machine cannot distribute the contents of your file across your cluster nodes to take advantage of parallel processing, which means that import performance will suffer significantly with <span class="CodeFont">gzip</span> files.

### []()Tip \#4:  Use Special Characters for Delimiters

One common gotcha we see with customer imports is when the data you're importing includes a special character that you've designated as a column or character delimiter. You'll end up with records in your bad record directory and can spend hours trying to determine the issue, only to discover that it's because the data includes a delimiter character. This can happen with columns that contain data such as product descriptions.

Column Delimiters

The standard column delimiter is a comma (<span class="CodeFont">,</span>); however, we've all worked with string data that contains commas, and have figured out to use a different column delimiter. Some customers use the pipe (<span class="CodeFont">|</span>) character, but frequently discover that it is also used in some descriptive data in the table they're importing.

We recommend using a control character like <span class="CodeFont">CTRL-A</span> for your column delimiter. This is known as the SOH character, and is represented by 0x01 in hexadecimal. Unfortunately, there's no way to enter this character from the keyboard in the Splice Machine command line interface; instead, you need to create a script file (see [Tip \#9](#Tip9)) and type the control character using a text editor like <span class="ItalicFont">vi</span> or <span class="ItalicFont">vim</span>:

-   Open your script file in vi or vim.
-   Enter into INSERT mode.
-   Type <span class="CodeFont">CTRL-V</span> then <span class="CodeFont">CTRL-A</span> for the value of the column delimiter parameter in your procedure call. Note that this typically echoes as <span class="CodeFont">^A</span> when you type it in vi or vim.

Character Delimiters

By default, the character delimiter is a double quote. This can produce the same kind of problems that we see with using a comma for the column delimiter: columns values that include embedded quotes or use the double quote as the symbol for inches. You can use escape characters to include the embedded quotes, but it's easier to use a special character for your delimiter.

We recommend using <span class="CodeFont">CTRL-G</span>, which you can add to a script file (see [Tip \#9](#Tip9)), again using a text editor like <span class="ItalicFont">vi</span> or <span class="ItalicFont">vim</span>:

-   Open your script file in vi or vim.
-   Enter into INSERT mode.
-   Type <span class="CodeFont">CTRL-V</span> then <span class="CodeFont">CTRL-G</span> for the value of the character delimiter parameter in your procedure call. Note that this typically echoes as <span class="CodeFont">^G</span> when you type it in vi or vim.

### []()Tip \#5:  Avoid Problems With Date, Time, and Timestamp Formats

Perhaps the most common difficulty that customers have with importing their data is with date, time, and timestamp values.

Splice Machine adheres to the Java <span class="CodeFont">SimpleDateFormat</span> syntax for all date, time, and timestamp values, <span class="CodeFont">SimpleDateFormat</span> is described here:

<https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html>

Splice Machine's implementation of <span class="CodeFont">SimpleDateFormat</span> is case-sensitive; this means, for example, that a lowercase <span class="CodeFont">h</span> is used to represent an hour value between 0 and 12, whereas an uppercase <span class="CodeFont">H</span> is used to represent an hour between 0 and 23.

Splice Machine's Import procedures only allow you to specify one format each for the date, time, and timestamp columns in the table data you are importing. This means that, for example, every date in the table data must be in the same format.

All of the <span class="CodeFont">Date</span> values in the file (or group of files) you are importing must use the same date format.

All of the <span class="CodeFont">Time</span> values in the file (or group of files) you are importing must use the same time format.

All of the <span class="CodeFont">Timestamp</span> values in the file (or group of files) you are importing must use the same timestamp format.

A few additional notes:

-   The <span class="CodeFont">Timestamp</span> data type has a range of <span class="CodeFont">1678-01-01</span> to <span class="CodeFont">2261-12-31</span>. Some customers have used dummy timestamp values like <span class="CodeFont">9999-01-01</span>, which will fail because the value is out of range for a timestamp. Note that this is not an issue with <span class="CodeFont">Date</span> values.
-   Splice Machine suggests that, if your data contains any date or timestamp values that are not in the format <span class="CodeFont">yyyy-MM-dd HH:mm:ss</span>, you create a simple table that has just one or two columns and test importing the format. This is a simple way to confirm that the imported data is what you expect.

### []()Tip \#6:  Change the Bad Directory for Each Table / Group

If you are importing a large amount of data and have divided the files you are importing into groups, then it's a good idea to change the location of the bad record directory for each group; this will make debugging bad records a lot easier for you.

You can change the value of the <span class="CodeFont">badRecordDirectory</span> to include your group name; for example, we typically use a strategy like the following:

| Group Files Location  | <span class="CodeBoldFont">badRecordDirectory</span> Parameter Value |
|-----------------------|----------------------------------------------------------------------|
| /data/mytable1/group1 | /BAD/mytable1/group1                                                 |
| /data/mytable1/group2 | /BAD/mytable1/group2                                                 |
| /data/mytable1/group3 | /BAD/mytable1/group3                                                 |

You'll then be able to more easily discover where the problem record is located.

### []()Tip \#7:  Importing Multi-line Records

If your data contains line feed characters like <span class="CodeFont">CTRL-M</span>, you need to set the <span class="CodeFont">oneLineRecords</span> parameter to <span class="CodeFont">false</span>. Splice Machine will accommodate to the line feeds; however, the import will take longer because Splice Machine will not be able to break the file up and distribute it across the cluster.

To improve import performance, avoid including line feed characters in your data and set the <span class="CodeFont">oneLineRecords</span> parameter to <span class="CodeFont">true</span>.

### []()Tip \#8:  Importing Clobs and Blobs

If you are importing <span class="CodeFont">CLOB</span>s, pay careful attention to tips [4](#Tip4) and [7](#Tip7). Be sure to use special characters for both your column and character delimiters. If your <span class="CodeFont">CLOB</span> data can span multiple lines, be sure to set the <span class="CodeFont">oneLineRecords</span> parameter to <span class="CodeFont">false</span>.

At this time, the Splice Machine import procedures do not import work with columns of type <span class="CodeFont">BLOB</span>. You can create a virtual table interface (VTI) that reads the <span class="CodeFont">BLOB</span>s and inserts them into your database.

### []()Tip \#9:  Scripting Your Imports

You can make import tasks much easier and convenient by creating <span class="ItalicFont">import scripts</span>. An import script is simply a call to one of the import procedures; once you've verified that it works, you can use and clone the script and run unattended imports.

An import script is simply a file in which you store <span class="CodeFont">splice&gt;</span> commands that you can execute with the <span class="CodeFont">run</span> command. For example, here's an example of a text file named <span class="CodeFont">myimports.sql</span> that we can use to import two csv files into our database:

``` Example
call SYSCS_UTIL.IMPORT_DATA ('SPLICE','mytable1',null,'/data/mytable1/data.csv',null,null,null,null,null,0,'/BAD/mytable1',null,null);
call SYSCS_UTIL.IMPORT_DATA ('SPLICE','mytable2',null,'/data/mytable2/data.csv',null,null,null,null,null,0,'/BAD/mytable2',null,null
```

To run an import script, use the <span class="CodeFont">splice&gt; run</span> command; for example:

``` Example
splice> run 'myimports.sql';
```

You can also start up the <span class="CodeFont">splice&gt;</span> command line interpreter with the name of a file to run; for example:

``` Example
sqlshell.sh -f myimports.sql
```

In fact, you can script almost any sequence of Splice Machine commands in a file and run that script within the command line interpreter or when you start the interpreter.

[]()Examples
------------

Note that these examples work for either importing or upserting data: you can simply substitute <span class="CodeFont">UPSERT\_DATA\_FROM\_FILE</span> in place of <span class="CodeFont">IMPORT\_DATA</span> in any of the system procedure calls below.

### Example 1: Importing data into a table with fewer columns than in the file

If the table into which you're importing data has less columns than the data file that you're importing, the "extra" data columns in the file are ignored. For example, if you create a table with this statement:

``` Example
CREATE TABLE playerTeams(ID int primary key, Team VARCHAR(32));
```

And your data file looks like this:

``` Example
1,Cards,Molina,Catcher
2,Giants,Posey,Catcher
3,Royals,Perez,Catcher
```

When you import the file into <span class="CodeFont">playerTeams</span>, only the first two columns are imported:

``` Example
call SYSCS_UTIL.IMPORT_DATA( 'SPLICE', 'playerTeams', null, 'myData.csv',
 null, null, null, null, null, 0, '/importErrsDir', true, null );

SELECT * FROM playerTeams ORDER by ID;
ID   |TEAM    
--------------
1    |Cards
2    |Giants
3    |Royals

3 rows selected
```

### Example 2: Importing a subset of data from a file into a table

This example uses the same table and import file as does the previous example, and it produces the same results, The difference between these two examples is that this one explicitly imports only the first two columns (which are named <span class="CodeFont">ID</span> and <span class="CodeFont">TEAM</span>) of the file:

``` Example
call SYSCS_UTIL.IMPORT_DATA( 'SPLICE','playerTeams', 'ID, TEAM', 'myData.csv',
 null, null, null, null, null, 0, 'importErrsDir', true, null );

SELECT * FROM playerTeams ORDER by ID;
ID   |TEAM    
--------------
1    |Cards
2    |Giants
3    |Royals

3 rows selected
```

### Example 3: Specifying a timestamp format for an entire table

Use a single timestamp format for the entire table by explicitly specifying a single <span class="CodeFont">timeStampFormat</span>.

``` Example
Mike,2013-04-21 09:21:24.98-05
Mike,2013-04-21 09:15:32.78-04
Mike,2013-03-23 09:45:00.68-05
```

You can then import the data with the following call:

``` Example
call SYSCS_UTIL.IMPORT_DATA('app','tabx','c1,c2',
    '/path/to/ts3.csv',
    ',', '''', 
    'yyyy-MM-dd HH:mm:ss.SSZ',
    null, null, 0, null, true, null);
```

Note that for any import use case shown above, the time shown in the imported table depends on the timezone setting where the data is imported. In other words, given the same csv file, if imported at locations with different time zones, the value in the table shown will be different. Additionally, daylight savings time may account for a 1-hour difference if timezone is specified.

 


