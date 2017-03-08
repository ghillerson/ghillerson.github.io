[Open topic with navigation](../../../index.html#Shared/Developers/FcnsAndProcs/WritingProcsAndFcns.html)

[]()[]()Writing Functions and Stored Procedures
===============================================

This topic shows you the steps required to write functions and stored procedures for use in your Splice Machine database.

-   Refer to the [Introduction to Functions and Stored Procedures](Intro.FcnsAndProcs.html) topic in this section for an overview and comparison of functions and stored procedures.
-   Refer to the [Storing and Updating Functions and Stored Procedures](StoringAndUpdatingFcnsAndProcs.html) topic in this section for information about storing your compiled code and updating the <span class="CodeFont">CLASSPATH</span> to ensure that Splice Machine can find your code.
-   Refer to the [Functions and Stored Procedure Examples](ProcAndFcnExamples.html) topic in this section for complete sample code for both a function and a stored procedure.

Note that the processes for adding functions and stored procedures to your Splice Machine database are quite similar; however, there are some important differences, so we've separated them into their own sections below.

Writing a Function in Splice Machine
------------------------------------

Follow the steps below to write a Splice Machine database function.

1.  Create a Java method

    Each function maps to a Java method. For example:

    ``` Example
    package com.splicemachine.cs.function;  

    public class Functions {
       public static int addNumbers(int val1, int val2) {
          return val1 + val2;
       }
    }
    ```

2.  Create the function in the database

    You can find the complete syntax for <span class="CodeFont">[CREATE FUNCTION](../../SQLReference/Statements/CreateFunction.html) </span>in the <span class="ItalicFont">Splice Machine SQL Reference</span> manual.

    Here's a quick example of creating a function. In this example, <span class="CodeFont">com.splicemachine.cs.function</span> is the package, <span class="CodeFont">Functions</span> is the class name, and <span class="CodeFont">addNumbers</span> is the method name:

    ``` Example
    CREATE FUNCTION add(val1 int, val2 int)
        RETURNS integer
        LANGUAGE JAVA
        PARAMETER STYLE JAVA
        NO SQL
        EXTERNAL NAME 'com.splicemachine.cs.function.Functions.addNumbers';
    ```

3.  Store your compiled Jar file and update your CLASSPATH

    Follow the instructions in the [Storing and Updating Functions and Stored Procedures](StoringAndUpdatingFcnsAndProcs.html) topic in this section to:

    -   store your Jar file
    -   update the class path so that Splice Machine can find your code when the function is called.

    Invoke your function

    You can invoke functions just like you would call any built-in database function. For example, if you're using the Splice Machine command line interface (<span class="ItalicFont">CLI</span>), and have created a function named <span class="CodeFont">add</span>, you could use a statement like the following:

    ``` AppCommand
    SELECT add(1,2) FROM SYS.SYSTABLES;
    ```

[]()Writing a Stored Procedure in Splice Machine
------------------------------------------------

Follow the steps below to write a Splice Machine database stored procedure.

1.  Write your custom stored procedure:

    Here is a very simple stored procedure that uses JDBC:

    You can use any Java IDE or text edit to write your code.

    You can find additional examples in the [Functions and Stored Procedure Examples](ProcAndFcnExamples.html) topic in this section.

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>See the information about [working with ResultSets](#ResultSet) in the next section.

2.  Compile your code and build a Jar file

    You now need to compile your stored procedure and build a jar file for it.

    You can use any Java IDE or build tool, such as <span class="ItalicFont">Maven</span> or <span class="ItalicFont">Ant</span>, to accomplish this. Alternatively, you can use the <span class="ItalicFont">javac</span> Java compiler and the <span class="ItalicFont">Java Archive</span> tool packaged with the JDK.

3.  Copy the Jar file to a cluster node

    Next, copy your custom Jar file to a region server (any node running an HBase region server) in your Splice Machine cluster. You can copy the file anywhere that allows the splice&gt; interface to access it.

    You can use any remote copying tool, such as scp or ftp. For example:

    ``` AppCommand
    scp custom-splice-procs-1.0.2-SNAPSHOT.jar splice@myServer:myDir
    ```

    See the [Storing and Updating Functions and Stored Procedures](StoringAndUpdatingFcnsAndProcs.html) topic in this section for more information.

4.  Deploy the Jar file to your cluster

    Deploying the Jar file requires you to install the file in your database, and to add it to your database's <span class="CodeFont">CLASSPATH</span>. You can accomplish both of these steps by calling built-in system procedures from the <span class="AppCommand">splice&gt;</span> command line interpreter. For example:

    ``` AppCommand
    CALL SQLJ.INSTALL_JAR('/Users/splice/my-directory-for-jar-files/custom-splice-procs-2.5-SNAPSHOT.jar', 'SPLICE.CUSTOM_SPLICE_PROCS_JAR', 0);

    CALL SYSCS_UTIL.SYSCS_SET_GLOBAL_DATABASE_PROPERTY('derby.database.classpath', 'SPLICE.CUSTOM_SPLICE_PROCS_JAR');
    ```

    The [<span class="CodeFont">SQLJ.INSTALL\_JAR</span>](../../SQLReference/BuiltInSysProcs/SQLJInstallJar.html) system procedure uploads the jar file from the local file system where <span class="AppCommand">splice&gt;</span> is executing into the HDFS:

    -   If you are running a cluster, the Jar files are stored under the <span class="CodeFont">/hbase/splicedb/jar</span> directory in HDFS (or MapR-FS).
    -   If you are running in standalone mode, the Jar files are stored on the local file system under the <span class="CodeFont">splicedb/jar</span> directory in the Splice install directory.

5.  Register your stored procedure with Splice Machine

    Register your stored procedure with the database by calling the <span class="CodeFont">[CREATE PROCEDURE](../../SQLReference/Statements/CreateProcedure.html)</span> statement. For example:

    ``` AppCommand
    CREATE PROCEDURE SPLICE.GET_TABLE_NAMES()
       PARAMETER STYLE JAVA
       READS SQL DATA
       LANGUAGE JAVA
       DYNAMIC RESULT SETS 1
       EXTERNAL NAME 'org.splicetest.customprocs.CustomSpliceProcs.GET_TABLE_NAMES';
    ```

    Note that after running the above <span class="CodeFont">CREATE PROCEDURE</span> statement, your procedure will show up in the list of available procedures when you run the Splice Machine <span class="AppCommand">show procedures</span> command.

    You can find the complete syntax for [<span class="CodeFont">CREATE PROCEDURE</span>](../../SQLReference/Statements/CreateProcedure.html) in the <span class="ItalicFont">Splice Machine SQL Reference</span> manual.

6.  Run your stored procedure

    You can run your stored procedure by calling it from the <span class="AppCommand">splice&gt;</span> prompt. For example:

    ``` AppCommand
    splice> call SPLICE.GET_TABLE_NAMES();
    ```

7.  Updating/Reloading your stored procedure

    If you make changes to your procedure's code, you need to create a new Jar file and reload that into your databaseby calling the <span class="CodeFont">SQLJ.REPLACE\_JAR</span> system procedure:

    ``` AppCommand
    CALL SQLJ.REPLACE_JAR('/Users/splice/my-directory-for-jar-files/custom-splice-procs-2.5-SNAPSHOT.jar', 'SPLICE.CUSTOM_SPLICE_PROCS_JAR');
    ```

[]()Working with ResultSets
---------------------------

Splice Machine follows the SQL-J part 1 standard for returning <span class="CodeFont">ResultSets</span> through Java procedures. Each <span class="CodeFont">ResultSet</span> is returned through one of the parameters passed to the java method. For example, the <span class="CodeFont">resultSet</span> parameter in the <span class="CodeFont">MY\_TEST\_PROC</span> method in our <span class="CodeFont">ExampleStoredProcedure</span> class:

``` Example
public class ExampleStoredProcedure {
   public static void MY_TEST_PROC(String myInput, ResultSet[] resultSet) throws SQLException {
     ...
   } 
}
```

Here are a set of things you should know about <span class="CodeFont">ResultSets\[\]</span> in stored procedures:

-   The <span class="CodeFont">ResultSets</span> are returned in the order in which they were created.
-   The <span class="CodeFont">ResultSets</span> must be open and generated from the <span class="CodeFont">jdbc:default:connection</span> default connection. Any other <span class="CodeFont">ResultSets</span> are ignored.
-   If you close the statement that created the <span class="CodeFont">ResultSet</span> within the procedure's method, that closes the <span class="CodeFont">ResultSet</span> you want. Instead, you can close the connection.
-   The Splice Machine database engine itself creates the one element <span class="CodeFont">ResultSet</span> arrays that hold the returned <span class="CodeFont">ResultSets</span>.
-   Although the [<span class="CodeFont">CREATE PROCEDURE</span>](../../SQLReference/Statements/CreateProcedure.html) call allows you to specify the number of <span class="CodeFont">DYNAMIC RESULT SETs</span>, we currently only support returning a single <span class="CodeFont">ResultSet</span>.

 


