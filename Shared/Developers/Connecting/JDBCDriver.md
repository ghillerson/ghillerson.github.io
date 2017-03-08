[Open topic with navigation](../../../index.html#Shared/Developers/Connecting/JDBCDriver.html)

Using the Splice Machine JDBC Driver[]()
========================================

This topic describes how to configure and use the Splice Machine JDBC driver, which you can use to connect with other databases and business tools that need to access your Splice Machine database; it also contains examples of configuring the JDBC driver with different programming languages. This topic contains these sections:

-   <a href="#Finding" class="MCXref xref">Finding the Driver</a> tells you how to access our JDBC driver.
-   <a href="#Connecti" class="MCXref xref">JDBC Driver Connection Parameters</a> describes the configuration parameters for our JDBC driver.
-   <a href="#Using" class="MCXref xref">Using the JDBC Driver with Java</a> contains a simple program that demonstrates the use of our JBDC driver with Java.
-   <a href="#Using2" class="MCXref xref">Using the JDBC Driver with Jython</a> contains a simple program that demonstrates the use of our JBDC driver with Jython.
-   <a href="#Using3" class="MCXref xref">Using the JDBC Driver with JRuby</a>contains a simple program that demonstrates the use of our JBDC driver with JRuby.

[]()Finding the Driver
----------------------

Our JDBC driver is automatically installed on your computer(s) when you install Splice Machine. You'll find it in the <span class="CodeFont">jdbc-driver</span> folder under the <span class="CodeFont">splicemachine</span> directory. Typical locations are:

| OS            | Driver Location                                                                                            |
|---------------|------------------------------------------------------------------------------------------------------------|
| Linux / MacOS | /splicemachine/jdbc-driver/<span class="PlatformVariablesJDBCDriverJar">db-client-2.0.1.18.jar</span>      |
| Windows       | C:\\splicemachine\\jdbc-driver\\<span class="PlatformVariablesJDBCDriverJar">db-client-2.0.1.18.jar</span> |

<span class="autonumber"><span class="noteAutoNum">IMPORTANT:  </span></span>You <span class="BoldFont">must</span> use the <span class="ItalicFont">Splice Machine</span> JDBC or ODBC drivers; other drivers will not work correctly.

[]()JDBC Driver Connection Parameters
-------------------------------------

You need to specify a few parameters to configure and/or connect with the JDBC driver; the following table shows the default values for connecting to Splice Machine:

| Connection Parameter | Default Value                                                                 | Comments                                                                                                                                                     |
|----------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| JDBC URL             | jdbc:splice://<span class="Highlighted">&lt;hostname&gt;</span>:1527/splicedb | Use <span class="CodeFont">localhost</span> as the <span class="HighlightedCode">&lt;hostname&gt;</span> value for the standalone version of Splice Machine. 
                                                                                                                                                                                                                                                                      
                                                                                                        On a cluster, specify the IP address of an HBase RegionServer.                                                                                                |
| JDBC driver class    | com.splicemachine.db.jdbc.ClientDriver                                        |                                                                                                                                                              |
| User name            | splice                                                                        | This is the default value; consult with your administrator for the value you should use.                                                                     |
| Password             | admin                                                                         | This is the default value; consult with your administrator for the value you should use.                                                                     |
| Database name        | splicedb                                                                      |                                                                                                                                                              |

[]()Using the JDBC Driver with Java
-----------------------------------

To use our JDBC driver with Java, you need to locate the Splice Machine client JAR file, which is automatically installed for you when you install Splice Machine. Follow the instructions in the previous section, <a href="#Connecti" class="MCXref xref">JDBC Driver Connection Parameters</a>, to configure your connection.

This section contains the <span class="CodeFont">SampleJDBC</span> program, which does the following:

-   connects to a standalone (<span class="CodeFont">localhost</span>) version of Splice Machine
-   creates a table named <span class="CodeFont">MYTESTTABLE</span>
-   inserts several sample records
-   issues a query to retrieve those records

### SampleJDBC

Here's a simple example program that uses our JDBC driver with Java:

1.  Copy the code:

    You can copy and paste the code below:

2.  Compile it:

    Compile and package the code into <span class="ShellCommand">splice-jdbc-test-0.0.1-SNAPSHOT.jar</span>.

3.  Run the program:

    When you run the program, your <span class="CodeFont">CLASSPATH</span> must include the path to the splice JDBC driver. If you did compile and package your code into <span class="CodeFont">splice-jdbc-test-<span class="PlatformVariablesSpliceJarVersionNum">2.0.0-SNAPSHOT.jar</span>-SNAPSHOT.jar</span>, you can run the program with this command line:

    ``` ShellCommand
    java -cp splice-installer-<platformVersion>/resources/jdbc-driver/db-client-2.0.1.18.jar com.splicemachine.cs.tools.SampleJDBC   
    ```

    The command should display a result like the following:

    ``` ShellCommand
    java -cp ./target/splice-cs-2.0.0-SNAPSHOT.jar-SNAPSHOT.jar com.splicemachine.cs.tools.SampleJDBC
    record=[1] a=[1] b=[a]
    record=[2] a=[2] b=[b]
    record=[3] a=[3] b=[c]
    record=[4] a=[4] b=[c]
    record=[5] a=[5] b=[c]
    ```

[]()Using the JDBC Driver with Jython
-------------------------------------

The sample program in this section, <span class="CodeFont">print\_tables.jy</span>, connects to Splice Machine, executes a query, and displays the retrieved results.

You must first:

-   Have Jython installed. You can download and install Jython by following the installation instructions in the Tutorials sections of the [Splice Community](https://community.splicemachine.com/) site.

-   Add the Splice client jar to your <span class="CodeFont">CLASSPATH</span>; for example:

    ``` ShellCommand
    export CLASSPATH=/splicemachine/jdbc-driver/db-client-2.0.1.18.jar
    ```

### print\_tables.jy

Here's a simple example program that uses our JDBC driver with Jython:

1.  Copy the code:

    You can copy and paste the code below:

2.  Save the code to <span class="CodeFont">print\_files.jy</span>.

3.  Run the program:

    Run the <span class="CodeFont">print\_tables.jy</span> program as follows:

    ``` ShellCommand
    jython print_tables.jy  
    ```

    The command should display a result like the following:

    ``` AppCommand
    Record=[1] id=[f9f140e7-0144-fcd8-d703-00003cbfba48] name=[ASDAS] type=[T]
    Record=[2] id=[c934c123-0144-fcd8-d703-00003cbfba48] name=[DDC_NOTMAILABLE] type=[T]
    Record=[3] id=[dd5cc163-0144-fcd8-d703-00003cbfba48] name=[FRANK_EMCONT_20130430] type=[T]
    Record=[4] id=[f584c1a3-0144-fcd8-d703-00003cbfba48] name=[INACTIVE_QA] type=[T]
    Record=[5] id=[cfcc41df-0144-fcd8-d703-00003cbfba48] name=[NUM_GROOM4] type=[T]
    Record=[6] id=[6b7f4217-0144-fcd8-d703-00003cbfba48] name=[PP_LL_QA] type=[T]
    Record=[7] id=[ac154287-0144-fcd8-d703-00003cbfba48] name=[QUAL_BRANDS] type=[T]
    Record=[8] id=[d67d42c7-0144-fcd8-d703-00003cbfba48] name=[SCIENCE_CAT_QA] type=[T]
    Record=[9] id=[c1e0c303-0144-fcd8-d703-00003cbfba48] name=[TESTOUTPUT2] type=[T]
    Record=[10] id=[f408c343-0144-fcd8-d703-00003cbfba48] name=[UAC_1267_AVJ] type=[T]
    ```

[]()Using the JDBC Driver with JRuby
------------------------------------

To use JRuby with Splice Machine, you need these software components:

-   JRuby itself, which you can read about and download from [http://jruby.org](http://jruby.org/).
-   The Ruby Version Manager (<span class="ItalicFont">RVM</span>), which provides the simple environment management capabilities to manage multiple Ruby environments.
-   The Splice Machine Derby JDBC driver.
-   The Rails <span class="CodeFont">activerecord-jdbcderby-adapter</span> gem (package).

### Configuring Splice Machine

You must assign the database connectivity parameters in the <span class="CodeFont">config/database.yml</span> file for your JRuby application. Your connectivity parameters should look like the following:

``` AppCommand
# Configure Using Gemfile
# gem 'activerecord-jdbcsqlite3-adapter'
# gem 'activerecord-jdbcderby-adapter'
#
development:
    adapter: jdbcderby
    database: splicedb
    username: splice
    password: admin
    driver: com.splicemachine.db.jdbc.ClientDriver
    url: jdbc:splice://localhost:1527/splicedb
```

### JRubyJDBC

Here's a simple example program that uses our JDBC driver with JRuby:

1.  Create the sample data table

    Create the <span class="CodeFont">MYTESTTABLE</span> table in your database and add a little test data. Your table should look something like the following:

    ``` AppCommand
    splice> describe SPLICE.MYTESTTABLE;


    COLUMN_NAME         |TYPE_NAME|DEC |NUM |COLUMN|COLUMN_DEF|CHAR_OCTE |IS_NULL
    ------------------------------------------------------------------------------
    A                   |INTEGER  |0   |10  |10    |NULL      |NULL      |YES     
    B                   |VARCHAR  |NULL|NULL|30    |NULL      |60        |YES     
     
    2 rows selected

    splice> select * from MYTESTTABLE order by A;

    A     |B
    ---------------------------
    1     |a
    2     |b
    3     |c
    4     |c
    5     |c

    5 rows selected
    ```

2.  Copy the code

    You can copy and paste the code below:

3.  Run the program

    Run the <span class="CodeFont">JRubyConnect</span> program as follows

    ``` ShellCommand
    jruby jrubyjdbc.rb   
    ```

    The command should display a result like the following:

    ``` AppCommand
    Record=[1] a=[3] b=[c]
    Record=[2] a=[4] b=[c]
    Record=[3] a=[5] b=[c]
    Record=[4] a=[1] b=[a]
    Record=[5] a=[2] b=[b]
    ```

 


