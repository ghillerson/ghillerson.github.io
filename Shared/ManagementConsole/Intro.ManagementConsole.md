[Open topic with navigation](../../index.html#Shared/ManagementConsole/Intro.ManagementConsole.html)

[]()Splice Machine Management Console Guide
===========================================

This topic introduces the <span class="ItalicFont">Splice Machine Management Console</span>, a browser-based tool that you can use to monitor database queries on your cluster in real time. The Console UI allows you to see the Spark queries that are currently running in Splice Machine on your cluster, and to then drill down into each job to see the current progress of the queries, and to identify any potential bottlenecks. If you see something amiss, you can also terminate a query.

The <span class="ItalicFont">Splice Machine Management Console</span> leverages the Spark cluster manager <span class="ItalicFont">Web UI</span>, which is described here: <http://spark.apache.org/docs/latest/monitoring.html>.

This chapter is organized into the following topics:

-   The next section, [About the Splice Machine Management Console](#About), tells you about the management console, including how to access it in your browser.
-   The [Features of the Splice Machine Management Console](ConsoleFeatures.html) topic describes how to use major features of the console interface.
-   The [Managing Queries with the Console](ManagingQueries.html) topic shows you how to review and monitor the progress of your Spark jobs.

[]()About the Splice Machine Management Console
-----------------------------------------------

The <span class="ItalicFont">Splice Machine Spark Management Console</span> is a browser-based tool that you can use to watch your active Spark queries execute and to review the execution of completed queries. You can use the console to:

-   View any completed jobs
-   Monitor active jobs as they execute
-   View a timeline chart of the events in a job and its stages
-   View a Directed Acyclic Graph (DAG) visualization of a job's stages and the tasks within each stage
-   Monitor persisted and cached storage in realtime

You can access the Splice Machine Management Console by pointing your browser at this URL:

``` AppCommand
http://localhost:4040
```

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The management console URL will only be active after you've run at least one query on our Spark engine; prior to using the Spark engine, your browser will report an error such as <span class="ItalicFont">Connection Refused</span>.

Here are some of the terms you'll encounter while using the management console:

| Term                  | Description                                                                                                                                                                                                                                                                                     |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Accumulators          | Accumulators are variables programmers can declare in Spark applications that can be efficiently supported in parallel operations, and are typically used to implement counters and sums.                                                                                                       |
| Additional Metrics    | You can indicate that you want to display additional metrics for a stage or job by clicking the <span class="AppCommand">Show Additional Metrics</span> arrow and then selecting which metrics you want shown.                                                                                  |
| DAG Visualization     | A visual depiction of the execution Directed Acyclic Graph (DAG) for a job or job stage, which shows the details and flow of data. You can click the <span class="AppCommand">DAG Visualization</span> arrow to switch to this view.                                                            |
| Enable Zooming        | For <span class="ItalicFont">event timeline</span> views, you can enable zooming to expand the view detail for a portion of the timeline. You can click the <span class="AppCommand">Event Timeline</span> arrow to switch to this view.                                                        |
| Event Timeline        | A view that graphically displays the sequence of all <span class="ItalicFont">jobs</span>, a specific job, or a <span class="ItalicFont">stage</span> within a job.                                                                                                                             |
| Executor              | A process that runs <span class="ItalicFont">tasks</span> on a cluster node.                                                                                                                                                                                                                    |
| GC Time               | The amount of time spent performing garbage collection in a stage.                                                                                                                                                                                                                              |
| Job                   | The basic unit of execution in the Spark engine, consisting of a set of stages. With some exceptions, each query submitted to the Spark engine is a single job.                                                                                                                                 
                                                                                                                                                                                                                                                                                                                          
                         Each job is assigned a unique Job Id and is part of a unique Job Group.                                                                                                                                                                                                                          |
| Locality Level        | To minimize data transfers, Spark tries to execute as close to the data as possible. The <span class="ItalicFont">Locality Level</span> value indicates whether a task was able to run on the local node.                                                                                       |
| Scheduling Mode       | The scheduling mode used for a job.                                                                                                                                                                                                                                                             
                                                                                                                                                                                                                                                                                                                          
                         In FIFO scheduling, the first job gets priority on all available resources while its stages have tasks to launch. Then the second job gets priority, and so on.                                                                                                                                  
                                                                                                                                                                                                                                                                                                                          
                         In FAIR scheduling, Spark assigns tasks between jobs in a round robin manner, meaning that all jobs get a roughly equal share of the available cluster resources. Which means that short jobs can gain fair access to resources immediately without having to wait for longer jobs to complete.  |
| Scheduling Pool       | The FAIR schedule groups jobs into pools, each of which can have a different priority weighting value, which allows you to submit jobs with higher or lower priorities.                                                                                                                         |
| ScrollInsensitive row | A row in a result set that is scrollable, and is not sensitive to changes committed by other transactions or by other statements in the same transaction.                                                                                                                                       |
| Shuffling             | Shuffling is the reallocation of data between multiple stages in a Spark job.                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                          
                         <span class="ItalicFont">Shuffle Write</span> is amount of data that is serialized and written at the end of a stage for transmission to the next stage. <span class="ItalicFont">Shuffle Read</span> is the amount of serialized data that is read at the beginning of a stage.                 |
| Stage                 | The Splice Machine Spark scheduler splits the execution of a <span class="ItalicFont">job</span> into stages, based on the RDD transformations required to complete the job.                                                                                                                    
                                                                                                                                                                                                                                                                                                                          
                         Each stage contains a group of tasks that perform a computation in parallel.                                                                                                                                                                                                                     |
| Task                  | A computational command sent from the application driver to an <span class="ItalicFont">executor</span> as part of a <span class="ItalicFont">stage</span>.                                                                                                                                     |

See Also
--------

-   [The Splice Machine In-Memory Engine](../../OnPremise/GettingStarted/InMemoryEngine.html)
-   [User Interface Features of the Splice Machine Management Console](ConsoleFeatures.html)
-   [Managing Queries with the Console](ManagingQueries.html)
-   [Using Spark Libraries with Splice Machine](../Developers/Fundamentals/SparkLibraries.html)

 


