[Open topic with navigation](../../index.html#Shared/CmdLineReference/CmdExport.html)

[]()Export Command
==================

The <span class="AppCommand">export</span> command exports the results of an SQL query to a CSV (comma separated value) file.

Syntax

``` FcnSyntax
EXPORT ( exportPath,
         compression,
         replicationCount,
         fileEncoding,
         fieldSeparator,
         quoteCharacter )  <SQL_QUERY>;
```

<span class="ItalicFont">exportPath</span>

The directory in which you want the export file(s) written.

<span class="ItalicFont">compress</span>

Whether or not to compress the exported files. You can specify one of the following values:

| Value | Description                                                                         |
|-------|-------------------------------------------------------------------------------------|
| true  | The exported files are compressed using <span class="CodeFont">deflate/gzip</span>. |
| false | Exported files are not compressed.                                                  |

<span class="ItalicFont">replicationCount</span>

The file system block replication count to use for the exported CSV files.

You can specify any positive integer value. The default value is <span class="CodeFont">1</span>.

<span class="ItalicFont">fileEncoding</span>

The character set encoding to use for the exported CSV files.

You can specify any character set encoding that is supported by the Java Virtual Machine (JVM). The default encoding is <span class="CodeFont">UTF-8</span>.

<span class="ItalicFont">fieldSeparator</span>

The character to use for separating fields in the exported CSV files.

The default separator character is the comma (<span class="CodeFont">,</span>).

<span class="ItalicFont">quoteCharacter</span>

The character to use for quoting output in the exported CSV files.

The default quote character is the double quotation mark (<span class="CodeFont">"</span>).

Usage

The <span class="AppCommand">EXPORT</span> command generates one or more CSV files and stores them in the directory that you specified in the <span class="CodeFont">exportPath</span> parameter. More than one output file is generated to enhance the parallelism and performance of this operation.

If <span class="CodeFont">compression=true</span>, then each of the generated files is named with this format:

``` AppCommand
export_<N>.csv.gz
```

If <span class="CodeFont">compression=false</span>, then each of the generated files is named with this format:

``` AppCommand
export_<N>.csv
```

The value of <span class="AppCommand">&lt;N&gt;</span> is a random integer value.

Merging the Exported Files

You can copy all of the exported files into a single file on your local file system using the Hadoop FS command <span class="CodeFont">getmerge</span>. The syntax for <span class="CodeFont">getmerge</span> is:

``` FcnSyntax
hadoop fs -getmerge sourceDir localPath
```

Use the <span class="ItalicFont">exportPath</span> directory as the value of sourceDir to copy all of the exported CSV files to your <span class="ItalicFont">localPath</span>.

For more information about the <span class="CodeFont">getmerge</span> command, see [http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/FileSystemShell.html\#getmerge.](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/FileSystemShell.html#getmerge)

Examples

``` AppCommand
         -- This example uses all default options:
 splice> EXPORT('/my/export/dir', false, null, null, null, null)
          SELECT a,b,sqrt(c) FROM t1 join t2 on t1.a=t2.a;

         -- This example explicitly specifies options:
splice> EXPORT('/my/export/dir', false, 3, 'utf-8', '|', ';')
          SELECT a,b,sqrt(c) FROM t1 join t2 on t1.a=t2.a;
```

 


