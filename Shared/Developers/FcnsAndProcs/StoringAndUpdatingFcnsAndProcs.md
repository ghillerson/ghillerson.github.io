[Open topic with navigation](../../../index.html#Shared/Developers/FcnsAndProcs/StoringAndUpdatingFcnsAndProcs.html)

Storing and Updating Splice Machine Functions and Stored Procedures
===================================================================

This topic describes how to store and update your compiled Java Jar (<span class="CodeFont">.jar</span>) files when developing stored procedures and functions for Splice Machine.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Jar files are not versioned: the <span class="CodeFont">GENERATIONID</span> is always zero. You can view the metadata for the Jar files in the Splice data dictionary by executing this query: <span class="CodeFont">select \* from sys.sysfiles;</span>

Adding a Jar File
-----------------

To add a new Jar file to your Splice Machine database, use the <span class="AppCommand">splice&gt;</span> command line interface to store the Jar and then update your <span class="CodeFont">CLASSPATH</span> property so that your code can be found:

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>When Splice Machine is searching for a class to load, it first searches the system <span class="CodeFont">CLASSPATH</span>. If the class is not found in the traditional system class path, Splice Machine then searches the class path set as the value of the <span class="CodeFont">derby.database.classpath</span> property.

1.  Load your Jar file into the Splice Machine database

    ``` AppCommand
    splice> CALL SQLJ.INSTALL_JAR('/Users/me/dev/workspace/examples/bin/example.jar', 'SPLICE.MY_EXAMPLE_APP', 0);
    ```

    Please refer to the <span class="CodeFont">[SQLJ.INSTALL\_JAR](../../SQLReference/BuiltInSysProcs/SQLJInstallJar.html)</span> topic in the Splice Machine SQL Reference book for more information about using this system procedure. To summarize:

    -   The first argument is the path on your computer to your Jar file.
    -   The second argument is the name for the stored procedure Jar file in your database, in <span class="CodeFont">schema.name</span> format.
    -   The third argument is currently unused but required; use <span class="CodeFont">0</span> as its value.

2.  Update your CLASSPATH

    You need to update your <span class="CodeFont">CLASSPATH</span> so that Splice Machine can find your code. You can do this by using the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY](../../SQLReference/BuiltInSysProcs/SetDatabaseProperty.html)</span> system procedure to update the <span class="CodeFont">derby.database.classpath</span> property:

    ``` AppCommand
    splice> CALL SYSCS_UTIL.SYSCS_SET_GLOBAL_DATABASE_PROPERTY('derby.database.classpath', 'SPLICE.MY_EXAMPLE_APP');
    ```

    Note that if you've developed more than one Jar file, you can update the <span class="CodeFont">derby.database.classpath</span> property with multiple Jars by separating the Jar file names with colons when you call the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY](../../SQLReference/BuiltInSysProcs/SetDatabaseProperty.html)</span> system procedure . For example:

    ``` AppCommand
    splice> CALL SYSCS_UTIL.SYSCS_SET_GLOBAL_DATABASE_PROPERTY('derby.database.classpath', 'SPLICE.MY_EXAMPLE_APP:SPLICE.YOUR_EXAMPLE');
    ```

Updating a Jar File
-------------------

You can use the <span class="AppCommand">splice&gt;</span> command line interface to replace a Jar file:

1.  Replace the stored Jar file

    ``` AppCommand
    splice> CALL SQLJ.REPLACE_JAR('/Users/me/dev/workspace/examples/bin/example.jar', 'SPLICE.MY_EXAMPLE_APP');
    ```

    Please refer to the <span class="CodeFont">[SQLJ.REPLACE\_JAR](../../SQLReference/BuiltInSysProcs/SQLJReplaceJar.html)</span> topic in the Splice Machine SQL Reference book for more information about using this system procedure. To summarize:

    -   The first argument is the path on your computer to your Jar file.
    -   The second argument is the name for the stored procedure Jar file in your database, in <span class="CodeFont">schema.name</span> format.

Deleting a Jar File
-------------------

You can use the <span class="AppCommand">splice&gt;</span> command line interface to delete a Jar file:

1.  Delete a stored Jar file

    ``` AppCommand
    splice> CALL SQLJ.REMOVE_JAR('SPLICE.MY_EXAMPLE_APP', 0);
    ```

    Please refer to the <span class="CodeFont">[SQLJ.REMOVE\_JAR](../../SQLReference/BuiltInSysProcs/SQLJRemoveJar.html)</span> topic in the Splice Machine SQL Reference book for more information about using this system procedure. To summarize:

    -   The first argument is the name for the stored procedure Jar file in your database, in <span class="CodeFont">schema.name</span> format.
    -   The second argument is currently unused but required; use <span class="CodeFont">0</span> as its value.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The Jar file operations (the <span class="CodeFont">[SQLJ.INSTALL\_JAR](../../SQLReference/BuiltInSysProcs/SQLJInstallJar.html)</span>, <span class="CodeFont">[SQLJ.REPLACE\_JAR](../../SQLReference/BuiltInSysProcs/SQLJReplaceJar.html)</span>, and <span class="CodeFont">[SQLJ.REMOVE\_JAR](../../SQLReference/BuiltInSysProcs/SQLJRemoveJar.html)</span> system procedures) are not executed within transactions, which means that committing or rolling back a transaction will not have any impact on these operations.

 


