[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/SQLJInstallJar.html)

<a href="" id="BuiltInSysProcs.SQLJInstallJar"></a>[]()SQLJ.INSTALL\_JAR
========================================================================

The <span class="CodeFont">SQLJ.INSTALL\_JAR</span> system procedure stores a jar file in a database.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>For more information about using JAR files, see the [Using Functions and Stored Procedures](../../Developers/FcnsAndProcs/Intro.FcnsAndProcs.html) section in our <span class="ItalicFont">Developer's Guide</span>.

Syntax

``` FcnSyntax
SQLJ.INSTALL_JAR(IN jar_file_path_or-url VARCHAR(32672),
                 IN qualified_jar_name VARCHAR(32672),
                 IN deploy INTEGER)
```

jar\_file\_path\_or-url

The path or URL of the jar file to add. A path includes both the directory and the file name (unless the file is in the current directory, in which case the directory is optional). For example:

``` Example
d:/todays_build/tours.jar
```

qualified\_jar\_name

Splice Machine name of the jar file, qualified by the schema name. Two examples:

``` Example
MYSCHEMA.Sample1
   -- a delimited identifier
MYSCHEMA."Sample2"
```

deploy

If this set to <span class="CodeFont">1</span>, it indicates the existence of an SQLJ deployment descriptor file. Splice Machine ignores this argument, so it is normally set to <span class="CodeFont">0</span>.

Usage Notes

This procedure will not work properly unless you have first added your procedure to the Derby CLASSPATH variable. For example:

``` Example
CALL SYSCS_UTIL.SYSCS_SET_GLOBAL_DATABASE_PROPERTY('derby.database.classpath', 'SPLICE.MY_EXAMPLE_APP');
```

For information about storing and updating stored procedures, and the setting of the Derby classpath, see the [Storing and Updating Splice Machine Functions and Stored Procedures](../../Developers/FcnsAndProcs/StoringAndUpdatingFcnsAndProcs.html) topic in our <span class="ItalicFont">Developer's Guide</span>.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

SQL Examples

``` Example
   -- Make sure Derby classpath variable is correctly set for our examples
CALL SYSCS_UTIL.SYSCS_SET_GLOBAL_DATABASE_PROPERTY('derby.database.classpath', 'SPLICE.SAMPLE1_APP:SPLICE.SAMPLE2');

   -- install jar from current directory
splice> CALL SQLJ.INSTALL_JAR('tours.jar', 'SPLICE.SAMPLE1_APP', 0);

   -- install jar using full path
splice> CALL SQLJ.INSTALL_JAR('c:\myjarfiles\tours.jar', 'SPLICE.SAMPLE1_APP', 0);

   -- install jar from remote location
splice> CALL SQLJ.INSTALL_JAR('http://www.example.com/tours.jar', 'SPLICE.SAMPLE2_APP', 0);

   -- install jar using a quoted identifier for the
   -- Splice Machine jar name
splice> CALL SQLJ.INSTALL_JAR('tours.jar', 'SPLICE."SAMPLE2"', 0);
```

See Also

-   [<span class="CodeFont">SQLJ\_REMOVE\_JAR</span>](SQLJRemoveJar.html)
-   [<span class="CodeFont">SQLJ\_REPLACE\_JAR</span>](SQLJReplaceJar.html)

 


