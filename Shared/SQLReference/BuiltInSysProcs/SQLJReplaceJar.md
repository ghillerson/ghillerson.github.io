[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/SQLJReplaceJar.html)

<a href="" id="BuiltInSysProcs.SQLJReplaceJar"></a>[]()SQLJ.REPLACE\_JAR
========================================================================

The <span class="CodeFont">SQLJ.REPLACE\_JAR</span> system procedure replaces a jar file in a database.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>For more information about using JAR files, see the [Using Functions and Stored Procedures](../../Developers/FcnsAndProcs/Intro.FcnsAndProcs.html) section in our <span class="ItalicFont">Developer's Guide</span>.

Syntax

``` FcnSyntax
SQLJ.REPLACE_JAR(
                IN jar_file_path_or-url VARCHAR(32672),
                IN qualified_jar_name VARCHAR(32672)
)
```

jar\_file\_path\_or-url

The path or URL of the jar file to use as a replacement. A path includes both the directory and the file name (unless the file is in the current directory, in which case the directory is optional). For example:

``` Example
d:/todays_build/tours.jar
```

qualified\_jar\_name

The Splice Machine name of the jar file, qualified by the schema name. Two examples:

``` Example
MYSCHEMA.Sample1
  -- a delimited identifier.
MYSCHEMA."Sample2"
```

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

SQL Example

``` Example
   -- SQL statement
CALL sqlj.replace_jar('c:\myjarfiles\newtours.jar', 'SPLICE.Sample1');
   
   -- SQL statement
   -- replace jar from remote location
CALL SQLJ.REPLACE_JAR('http://www.example.com/tours.jar', 'SPLICE.Sample2');
```

See Also

-   [<span class="CodeFont">SQLJ\_INSTALL\_JAR</span>](SQLJInstallJar.html)
-   [<span class="CodeFont">SQLJ\_REMOVE\_JAR</span>](ModifyPassword.html)

 


