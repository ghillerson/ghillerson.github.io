[Open topic with navigation](../../index.html#OnPremise/Administrators/ShuttingDownDatabase.html)

Shutting DownYour Database
==========================

This topic describes how to shut down your Splice Machine database. You need to follow different steps, depending on which version of Splice Machine you are using:

-   [Shutting Down Your Splice Machine Database on a Cloudera-Managed Cluster](#ShutdownDBCloudera)
-   [Shutting Down Your Splice Machine Database on a Hortonworks HDP-Managed Cluster](#ShutdownDBHDP)
-   [Shutting Down Your Splice Machine Database on a MapR-Managed Cluster](#ShutdownDBMapR)
-   [Shutting Down Your Splice Machine Database on a Standalone installation](#ShutdownDbStandalone)

[]()[]()Shutting Down Your Splice Machine Database on a Cloudera-Managed Cluster
--------------------------------------------------------------------------------

Use the Cloudera Manager to either shut down HBase or to shut down the entire cluster, whichever is appropriate for your situation.

1.  Navigate to the <span class="ItalicFont">Services-&gt;All Services</span> screen in <span class="ItalicFont">Cloudera Manager</span>, and select this action to stop <span class="ItalicFont">HBase</span>:

    ``` AppCommand
    hbase -> Actions -> Stop
    ```

2.  If you also want to shut down the entire cluster, select this action in the same screen to stop<span class="ItalicFont">HDFS</span>:

    ``` AppCommand
    hdfs1 -> Actions -> Stop
    ```

[]()[]()Shutting Down Your Splice Machine Database on a Hortonworks HDP-Managed Cluster
---------------------------------------------------------------------------------------

Use the Ambari dashboard to shut down Splice Machine:

1.  Log in to the Ambari Dashboard by pointing your browser to the publicly visible <span class="HighlightedCode">&lt;hostName&gt;</span> for your master node that is hosting Ambari Server:

    ``` ShellCommand
    http://<hostName>:8080/
    ```

2.  Shut down cluster services by selecting:

    ``` AppCommand
    Action -> Stop All
    ```

[]()[]()Shutting Down Your Splice Machine Database on a MapR-Managed Cluster
----------------------------------------------------------------------------

To shut down Splice Machine, use the MapR Command System (MCS) to stop HBase.

1.  Navigate to the node that is running the <span class="CodeFont">mapr-webserver</span> service.
2.  Log into <span class="CodeFont">https://<span class="HighlightedCode">&lt;hostIPAddr&gt;</span>:8443</span>, substituting the correct <span class="HighlightedCode">&lt;hostIPAddr&gt;</span> value.
3.  Stop hbase.

[]()Shutting Down Your Database in the Standalone Version[]()
-------------------------------------------------------------

Follow these steps to shut down your database if you're using the Standalone version of Splice Machine:

1.  Make sure that you have quit the <span class="AppCommand">splice&gt;</span> command line interpreter:

    ``` AppCommand
    splice> quit;
    ```

2.  Change directory to your install directory:

    ``` ShellCommand
    cd splicemachine
    ```

3.  Run the following scripts:

    ``` ShellCommand
    $ ./bin/stop-splice.sh
    ```

This stops the Splice Machine database and the Splice Machine Administrative Console.

 


