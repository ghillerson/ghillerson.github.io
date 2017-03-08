[Open topic with navigation](../../../index.html#Shared/Developers/Fundamentals/SparkLibraries.html)

[]()Using Spark Libraries with Splice Machine
=============================================

One of the great features of Spark is that a large number of libraries have been and continue to be developed for use with Spark. This topic provides an example of interfacing to the Spark Machine Learning library (MLlib).

You can follow a similar path to interface with other Spark libraries, which involves these steps:

1.  Create a class with an API that leverages functionality in the Spark library you want to use.
2.  Write a custom procedure in your Splice Machine database that converts a Splice Machine result set into a Spark Resilient Distributed Dataset (RDD).
3.  Use the Spark library with the RDD.

Example: Using Spark MLlib with Splice Machine Statistics
---------------------------------------------------------

This section presents the sample code for interfacing Splice Machine with the Spark Machine Learning Library (MLlib), in these subsections:

-   [About the Splice Machine SparkMLibUtils Class API](#About) describes the SparkMLibUtils class that Splice Machine provides for interfacing with this library.
-   [Creating our SparkStatistics Example Class](#Create) summarizes the <span class="CodeFont">SparkStatistics</span> Java class that we created for this example.
-   [Run a Sample Program to Use Our Class](#Run) shows you how to define a custom procedure in your database to interface to the <span class="CodeFont">SparkStatistics</span> class.

### []()About the Splice Machine SparkMLibUtils Class API

Our example makes use of the Splice Machine <span class="CodeFont">com.splicemachine.example.SparkMLibUtils</span> class, which you can use to interface between your Splice Machine database and the Spark Machine Learning library.

Here's are the public methods from the <span class="CodeFont">SparkMLibUtils</span> class:

> resultSetToRDD
>
> Converts a Splice Machine result set into a Spark Resilient Distributed Dataset (RDD) object.
>
> locatedRowRDDToVectorRDD
>
> Transforms an RDD into a vector for use with the Machine Learning library. The <span class="CodeFont">fieldsToConvert</span> parameter specifies which column positions to include in the vector.
>
> convertExecRowToVector
>
> Converts a Splice Machine <span class="CodeFont">execrow</span> into a vector. The <span class="CodeFont">fieldsToConvert</span> parameter specifies which column positions to include in the vector.

### []()Creating our SparkStatistics Example Class

For this example, we define a Java class named SparkStatistics that can query a Splice Machine table, convert that results into a Spark JavaRDD, and then use the Spark MLlib to calculate statistics.

Our class, <span class="CodeFont">SparkStatistics</span>, defines one public interface:

We call the <span class="CodeFont">getStatementStatistics</span> from custom procedure in our database, passing it an SQL query . <span class="CodeFont">getStatementStatistics</span> performs the following operations:

1.  Query your database

    The first step is to use our JDBC driver to connect to your database and run the query:

    ``` Example
    Connection con = DriverManager.getConnection("jdbc:default:connection");
    PreparedStatement ps = con.prepareStatement(statement);
    ResultSet rs = ps.executeQuery();
    ```

2.  Convert the query results into a Spark RDD

    Next, we convert the query's result set into a Spark RDD:

    ``` Example
    JavaRDD<LocatedRow> resultSetRDD = ResultSetToRDD(rs);
    ```

3.  Calculate statistics

    Next, we use Spark to collect statistics for the query, using private methods in our <span class="CodeFont">SparkStatistics</span> class:

    ``` Example
    int[] fieldsToConvert = getFieldsToConvert(ps);
    MultivariateStatisticalSummary summary = getColumnStatisticsSummary(resultSetRDD, fieldsToConvert);
    ```

    You can view the implementations of the <span class="CodeFont">getFieldsToConvert</span> and <span class="CodeFont">getColumnStatisticsSummary</span> methods in the <span class="ItalicFont">[Appendix](#Appendix)</span> at the end of this topic.

4.  Return the results

    Finally, we return the results:

    ``` Example
    IteratorNoPutResultSet resultsToWrap = wrapResults((EmbedConnection) con, getColumnStatistics(ps, summary, fieldsToConvert));
    resultSets[0] = new EmbedResultSet40((EmbedConnection)con, resultsToWrap, false, null, true);
    ```

 

### []()Run a Sample Program to Use Our Class

Follow these steps to run a simple example program to use the Spark MLlib library to calculate statistics for an SQL statement.

1.  Create Your API Class

    The first step is to create a Java class that uses Spark to generate and analyze statistics, as shown in the previous section, [Creating our SparkStatistics Example Class](#Create)

2.  Create your custom procedure

    First we create a procedure in our database that references the <span class="CodeFont">getStatementStatistics</span> method in our API, which takes an SQL query as its input and uses Spark to calculate statistics for the query using MLlib:

    ``` Example
    CREATE PROCEDURE getStatementStatistics(statement varchar(1024)) 
       PARAMETER STYLE JAVA
       LANGUAGE JAVA 
       READS SQL DATA 
       DYNAMIC RESULT SETS 1 
       EXTERNAL NAME 'com.splicemachine.example.SparkStatistics.getStatementStatistics';
    ```

3.  Create a table to use

    Let's create a very simple table to illustrate use of our procedure:

    ``` Example
    create table t( col1 int, col2 double);
    insert into t values(1, 10);
    insert into t values(2, 20);
    insert into t values(3, 30);
    insert into t values(4, 40);
    ```

4.  Call your custom procedure to get statistics

    Now call your custom procedure, which sends an SQL statement to the SparkStatistics class we created to generate a result set:

    ``` Example
    call splice.getStatementStatistics('select * from t');
    ```

[]()Appendix: The SparkStatistics Class
---------------------------------------

Here's the full code for our SparkStatistics class:

See Also
--------

-   [The Splice Machine In-Memory Engine](../../../OnPremise/GettingStarted/InMemoryEngine.html)
-   [Using the Splice Machine Management Console](../../ManagementConsole/Intro.ManagementConsole.html)
-   You can find the Spark MLlib guide in the Programming Guides section of the Spark documentation site: <https://spark.apache.org/docs>

 


