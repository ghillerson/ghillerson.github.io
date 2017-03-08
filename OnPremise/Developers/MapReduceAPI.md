[Open topic with navigation](../../index.html#OnPremise/Developers/MapReduceAPI.html)

Splice Machine Map Reduce API
=============================

The Splice Machine MapReduce API provides a simple programming interface to the Map Reduce Framework that is integrated into Splice Machine. You can use MapReduce to import data, export data, or for purposes such as implementing machine learning algorithms. One likely scenario for using the Splice Machine MapReduce API is for customers who already have a Hadoop cluster, want to use Splice Machine as their transactional database, and need to continue using their batch MapReduce jobs.

This topic includes a summary of the Java classes included in the API, and [presents an example](#Example) of using the MapReduce API.

Splice Machine MapReduce API Classes
------------------------------------

The Splice Machine MapReduce API includes the following key classes:

| Class               | Description                                                                                                                                                                 |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SpliceJob           | Creates a transaction for the MapReduce job.                                                                                                                                |
| SMInputFormat       | Creates an object that:                                                                                                                                                     
                                                                                                                                                                                                    
                       -   uses Splice Machine to scan the table and decode the data                                                                                                                
                       -   returns an <span class="CodeFont">ExecRow</span> (typed data) object                                                                                                     |
| SMOutputFormat      | Creates an object that:                                                                                                                                                     
                                                                                                                                                                                                    
                       -   writes to a buffered cache                                                                                                                                               
                       -   dumps the cache into Splice Machine                                                                                                                                      
                       -   returns an <span class="CodeFont">ExecRow</span> (typed data) object.                                                                                                    |
| SpliceMapReduceUtil | A Helper class for writing MapReduce jobs in java; this class is used to initiate a mapper job or a reducer job, to set the number of reducers, and to add dependency jars. |

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Each transaction must manage its own commit and rollback operations.

For information about and examples of using Splice Machine with HCatalog, see the Using Splice Machine with HCatalog topic in this book.

[]()Example of Using the Splice Machine MapReduce API
-----------------------------------------------------

This topic describes using the Splice Machine MapReduce API, <span class="CodeFont">com.splicemachine.mrio.api</span>, a simple word count program that retrieves data from an input table, summarizes the count of initial character of each word, and writes the result to an output table.

1.  Define your input and output tables:

    First, assign the name of the Splice Machine database table from which you want to retrieve data to a variable, and then assign a name for your output table to another variable:

    ``` Example
    String inputTableName  = "WIKIDATA";
    String outputTableName = "USERTEST";
    ```

    You can specify table names using the <span class="ItalicFont">&lt;schemaName&gt;.&lt;tableName&gt;</span> format; if you don't specify a schema name, the default schema is assumed.

2.  Create a new job instance:

    You need to create a new job instance and assign a name to it:

    ``` Example
    Configuration config = HBaseConfiguration.create();
    Job job = new Job(config, "WordCount");
    ```

3.  Initialize your mapper job:

    We initialize our sample job using the <span class="CodeFont">initTableMapperJob</span> utility method:

4.  Retrieve values within your map function:

    Our sample <span class="CodeFont">map</span> function retrieves and parses a single row with specified columns.

5.  Manipulate and save the value with reduce function:

    Our sample <span class="CodeFont">reduce</span> function manipulates and saves the value by creating an <span class="CodeFont">ExecRow</span> and filling in the row with the <span class="CodeFont">execRow.setRowArray</span> method.

6.  Commit or rollback the job:

    If the job is successful, commit the transaction.

    ``` Example
    job.commit();
    ```

    If the job fails, roll back the transaction.

    ``` Example
    job.rollback();
    ```

 


