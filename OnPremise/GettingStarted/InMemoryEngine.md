[Open topic with navigation](../../index.html#OnPremise/GettingStarted/InMemoryEngine.html)

[]()The Splice Machine In-Memory Engine
=======================================

This topic provides an overview of the Splice Machine in-memory engine, which tremendously boosts OLAP (analytical) query performance. Splice Machine use Apache™ Spark as our in-memory engine and automatically detects and directs OLAP queries to that engine.

This topic presents a very brief overview of Spark terminology and concepts.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If you're not yet familiar with Spark, we recommend visiting the Apache Spark web site, [spark.apache.org](http://spark.apache.org/), to learn the basics, and for links to the official Spark documentation.

Spark Overview
--------------

Apache Spark is an open source computational engine that manages tasks in a computing cluster. Spark was originally developed at UC Berkeley in 2009, and then open sourced in 2010 as an Apache project. Spark has been engineered from the ground up for performance, exploiting in-memory computing and other optimizations to provide powerful analysis on very large data sets.

Spark provides numerous performance-oriented features, including:

-   ability to cache datasets in memory for interactive data analysis
-   abstraction
-   integration with a host of data sources
-   very fast data analysis
-   easy to use APIs for operating on large datasets, including numerous operators for transforming and manipulating data, in Java, Scala, Python, and other languages
-   numerous high level libraries, including support for machine learning, streaming, and graph processing
-   scalability to thousands of nodes

Spark applications consist of a driver program and some number of worker programs running on cluster nodes. The data sets (RDDs) used by the application are distributed across the worker nodes.

Spark Terminology
-----------------

Splice Machine launches Spark queries on your cluster as Spark <span class="ItalicFont">jobs</span>, each of which consists of some number of <span class="ItalicFont">stages</span>. Each stage then runs a number of <span class="ItalicFont">tasks</span>, each of which is a unit of work that is sent to an <span class="ItalicFont">executor</span>.

The table below contains a brief glossary of the terms you'll see when using the Splice Machine Management Console:

| Term           | Definition                                                                                                                                                                                                                                                                                                                                                    |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Action         | A function that returns a value to the driver after running a computation on an <span class="ItalicFont">RDD</span>. Examples include <span class="CodeFont">save</span> and <span class="CodeFont">collect</span> functions.                                                                                                                                 |
| Application    | A user program built on Spark. Each application consists of a <span class="ItalicFont">driver program</span> and a number of <span class="ItalicFont">executors</span> running on your cluster.                                                                                                                                                               
                                                                                                                                                                                                                                                                                                                                                                                 
                  An application creates <span class="ItalicFont">RDDs</span>, transforms those RDDs, and runs <span class="ItalicFont">actions</span> on them. These result in a directed acyclic graph (DAG) of operations, which is compiled into a set of <span class="ItalicFont">stages</span>. Each stage consists of a number of <span class="ItalicFont">tasks</span>.  |
| DAG            | A <span class="BoldFont">D</span>irected <span class="BoldFont">A</span>cyclic <span class="BoldFont">G</span>raph of the operations to run on an RDD.                                                                                                                                                                                                        |
| Driver program | This is the process that's running the <span class="CodeFont">main()</span> function of the application and creating the <span class="CodeFont">SparkContext</span> object, which sends jobs to <span class="ItalicFont">executors</span>.                                                                                                                    |
| Executor       | A process that is launched (by the driver program) for an <span class="ItalicFont">application</span> on a <span class="ItalicFont">worker node</span>. The executor launches <span class="ItalicFont">tasks</span> and maintains data for them.                                                                                                              |
| Job            | A parallel computation consisting of multiple <span class="ItalicFont">tasks</span> that gets spawned in response to a Spark <span class="ItalicFont">action</span>.                                                                                                                                                                                          |
| Partition      | A subset of the elements in an <span class="ItalicFont">RDD</span>. Partitions define the unit of parallelism; Spark processes elements within a partition in sequence and multiple partitions in parallel.                                                                                                                                                   |
| RDD            | A <span class="BoldFont">R</span>esilient <span class="BoldFont">D</span>istributed <span class="BoldFont">D</span>ataset. This is the core programming abstraction in Spark, consisting of a fault-tolerant collection of elements that can be operated on in parallel.                                                                                      |
| Stage          | A set of tasks that run in parallel. The stage creates a <span class="ItalicFont">task</span> for each partition in an <span class="ItalicFont">RDD</span>, serializes those tasks, and sends those tasks to <span class="ItalicFont">executors</span>.                                                                                                       |
| Task           | The fundamental unit of work in Spark; each task fetches input, executes operations, and generates output.                                                                                                                                                                                                                                                    |
| Transformation | A function that creates a new <span class="ItalicFont">RDD</span> from an existing <span class="ItalicFont">RDD</span>.                                                                                                                                                                                                                                       |
| Worker node    | A cluster node that can run application code.                                                                                                                                                                                                                                                                                                                 |

See Also
--------

-   [About the Splice Machine Management Console](../../Shared/ManagementConsole/Intro.ManagementConsole.html)
-   [User Interface Features of the Splice Machine Management Console](../../Shared/ManagementConsole/ConsoleFeatures.html)
-   [Managing Queries with the Console](../../Shared/ManagementConsole/ManagingQueries.html)
-   [Using Spark Libraries with Splice Machine](../../Shared/Developers/Fundamentals/SparkLibraries.html)
-   The Apache Spark web site, [spark.apache.org](http://spark.apache.org/)

 

 


