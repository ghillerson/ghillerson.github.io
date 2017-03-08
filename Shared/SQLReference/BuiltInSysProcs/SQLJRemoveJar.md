[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/SQLJRemoveJar.html)

<a href="" id="BuiltInSysProcs.SQLJRemoveJar"></a>[]()SQLJ.REMOVE\_JAR
======================================================================

The <span class="ItalicFont">SQLJ.REMOVE\_JAR</span> system procedure removes a jar file from a database.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>For more information about using JAR files, see the [Using Functions and Stored Procedures](../../Developers/FcnsAndProcs/Intro.FcnsAndProcs.html) section in our <span class="ItalicFont">Developer's Guide</span>.

Syntax

``` FcnSyntax
SQLJ.REMOVE_JAR(
        IN qualified_jar_name VARCHAR(32672),
        IN undeploy INTEGER
        )
```

qualified\_jar\_name

The Splice Machine name of the jar file, qualified by the schema name. Two examples:

``` Example
MYSCHEMA.Sample1
   -- a delimited identifier.
MYSCHEMA."Sample2"
```

undeploy

If set to <span class="CodeFont">1</span>, this indicates the existence of an SQLJ deployment descriptor file. Splice Machine ignores this argument, so it is normally set to <span class="CodeFont">0</span>.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

SQL Example

``` Example
-- SQL statement
CALL SQLJ.REMOVE_JAR('SPLICE.Sample1', 0);
```

See Also

-   [<span class="CodeFont">SQLJ\_INSTALL\_JAR</span>](SQLJInstallJar.html)
-   [<span class="CodeFont">SQLJ\_REPLACE\_JAR</span>](SQLJReplaceJar.html)

 


