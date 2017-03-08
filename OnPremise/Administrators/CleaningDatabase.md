[Open topic with navigation](../../index.html#OnPremise/Administrators/CleaningDatabase.html)

Cleaning Your Database
======================

Cleaning your database essentially wipes out any user-defined tables, indexes, and related items. You need to follow different steps, depending on which version of Splice Machine you are using:

-   [Cleaning Your Splice Machine Database on a Cloudera-Managed Cluster](#CleaningDBCloudera)
-   [Cleaning Your Splice Machine Database on a Hortonworks HDP-Managed Cluster](#CleaningDBHDP)
-   [Cleaning Your Splice Machine Database on a MapR-Managed Cluster](#CleaningDBMapR)
-   [Cleaning Your Splice Machine Database on a Standalone installation](#CleaningDbStandalone)

[]()[]()Cleaning Your Splice Machine Database on a Cloudera-Managed Cluster
---------------------------------------------------------------------------

Follow these steps to clean your database if you're using the Cloudera-managed cluster version of Splice Machine:

1.  Shut down HBase and HDFS

    Navigate to the <span class="AppCommand">Services-&gt;All Services</span> screen in <span>Cloudera Manager</span>, and select these actions to stop <span class="ItalicFont">HBase</span> and <span class="ItalicFont">HDFS</span>:

    ``` AppCommand
    hbase -> Actions -> Stop
    hdfs1 -> Actions -> Stop
    zookeeper1 -> Actions -> Stop
    ```

2.  Use the Zookeeper client to clean things:

    Restart ZooKeeper in the <span class="AppCommand">Services-&gt;All Services</span> screen:

    ``` AppCommand
    zookeeper1 -> Actions -> Start
    ```

    Log in to the machine running Zookeeper on your cluster and start up a command-line (terminal) window.

    Run the <span class="ShellCommand">zookeeper-client</span> command. At the prompt, run the following commands:

    ``` AppCommand
    rmr /startupPath
    rmr /spliceJobs
    rmr /derbyPropertyPath
    rmr /spliceTasks
    rmr /hbase
    rmr /conglomerates
    rmr /transactions
    rmr /ddl
    ```

3.  Start HDFS

    Navigate to the <span class="AppCommand">Services-&gt;All Services</span> screen in <span>Cloudera Manager</span>, and restart <span class="ItalicFont">HDFS</span>:

    ``` AppCommand
    hdfs1 -> Actions -> Start
    ```

4.  Clean up HBase

    []()Use the following shell command to delete the existing <span class="CodeFont">/hbase</span> directory. You can run this command on any Data Node:

    ``` ShellCommand
    sudo -su hdfs hadoop fs -rm -r /hbase
    ```

    If you are logged in as root, use this command instead:

    ``` ShellCommand
    sudo -u hdfs hadoop fs -rm -r /hbase
    ```

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>If the machine running Cloudera Manager is not part of the cluster, <span class="BoldFont">do not</span> run the command on that machine

5.  Create a new HBase directory:

    Navigate to the <span class="AppCommand">HBase</span> screen in <span>Cloudera Manager</span>, and create a new <span class="CodeFont">/hbase</span> directory by selecting:

    ``` AppCommand
    Actions -> Create Root Directory
    ```

6.  Restart HBase

    Now restart HBase from the same <span class="AppCommand">Home-&gt;Services-&gt;hbase1</span> screen in Cloudera Manager, using this action:

    ``` AppCommand
    Actions -> Start
    ```

[]()[]()Cleaning Your Splice Machine Database on a Hortonworks HDP-Managed Cluster
----------------------------------------------------------------------------------

Follow these steps to clean (or <span class="ItalicFont">flatten</span>) your database if you're using Splice Machine on an Ambari-managed Hortonworks Cluster:

1.  Shut down HBase and HDFS

    Log in to the Ambari Dashboard by pointing your browser to the publicly visible <span class="HighlightedCode">&lt;hostName&gt;</span> for your master node that is hosting Ambari Server:

    ``` ShellCommand
    http://<hostName>:8080/
    ```

    > ``` ShellCommand
    > http://<hostName>:8080/
    > ```
    >
    Select these actions to stop HBase and HDFS: :

    ``` AppCommand
    Services->HBase->Service Actions->Stop
    Services->HDFS->Service Actions->Stop
    ```

2.  Use the Zookeeper client to clean things

    Log in to the node running Zookeeper on your cluster and start up a command-line (terminal) window.

    Run the <span class="ShellCommand">zookeeper-client</span> command. At the prompt, run the following commands:

    ``` AppCommand
    rmr /startupPath
    rmr /spliceJobs
    rmr /derbyPropertyPath
    rmr /spliceTasks
    rmr /hbase-unsecure
    rmr /conglomerates
    rmr /transactions
    rmr /ddl
    ```

3.  Restart HDFS

    Use the Ambari Dashboard to restart HDFS:

    ``` AppCommand
    Services->HDFS->Service Actions->Start
    ```

4.  Re-create the required directory structure

    You need to SSH into a node that is running the HDFS Client and re-create the directory structure that Splice Machine expects by issuing these commands:

    Run the <span class="ShellCommand">zookeeper-client</span> command. At the prompt, run the following commands:

    ``` ShellCommand
    sudo -su hdfs hadoop fs -rm -r /apps/hbase
    sudo -su hdfs hadoop fs -mkdir /apps/hbase
    sudo -su hdfs hadoop fs -mkdir /apps/hbase/data
    sudo -su hdfs hadoop fs -chown hbase:hdfs /apps/hbase
    sudo -su hdfs hadoop fs -chown hbase:hdfs /apps/hbase/data
    ```

5.  Restart HBase

    Use the Ambari Dashboard to restart HBase:

    ``` AppCommand
    Services->HBase->Service Actions->Start
    ```

[]()[]()Cleaning Your Splice Machine Database on a MapR-Managed Cluster
-----------------------------------------------------------------------

Follow the steps below to clean (flatten) your database on your MapR cluster. You must be logged in as the cluster administrator (typically <span class="CodeFont">clusteradmin</span> or <span class="CodeFont">ec2-user</span>) to run each step. Unless otherwise specified, run each of these steps <span class="BoldFont">on your cluster control node</span>; some steps, as indicated, must be run on each node in your cluster.

1.  Stop the HBase RegionServers and Master:

    Use the following command <span class="BoldFont">on your control node</span> to stop HBase on your cluster:

    ``` AppCommand
    ~/splice-installer-mapr4.0/stop-hbase.sh
    ```

2.  Remove old data from HDFS:

    Ignore any error messages you may see when you run this command:

    ``` AppCommand
    sudo -iu mapr hadoop fs -rm -r -f 'maprfs:///hbase/*'
    ```

3.  Stop MapR warden services:

    Run the following command <span class="BoldFont">on each node</span> in your cluster:

    ``` AppCommand
    sudo service mapr-warden stop
    ```

4.  Launch the ZooKeeper command line shell:

    Note that the exact path may vary with different MapR versions

    ``` AppCommand
    /opt/mapr/zookeeper/zookeeper-3.4.5/bin/zkCli.sh
    ```

5.  Connect to the local ZooKeeper instance:

    When the ZooKeeper command shell prompts you, enter the <span class="HighlightedCode">connect</span> command shown here:

    ``` AppCommand
    Connecting to localhost:2181
    Welcome to ZooKeeper!
    JLine support is enabled
    [zk: localhost:2181(CONNECTING) 0] connect localhost:5181
    ```

6.  Complete the connection:

    Press <span class="CodeFont">Enter</span> again to display the connected prompt

    ``` AppCommand
    [zk: localhost:5181(CONNECTED) 1]
    ```

7.  Clear old ZooKeeper data:

    Enter the following commands to clear ZooKeeper data and then exit the command shell:

    ``` AppCommand
    rmr /startupPath
    rmr /spliceJobs
    rmr /derbyPropertyPath
    rmr /spliceTasks
    rmr /hbase
    rmr /conglomerates
    rmr /transactions
    rmr /ddl
    quit
    ```

8.  Restart MapR warden services on all nodes:

    Run the following command <span class="BoldFont">on each node</span> in your cluster:

    ``` AppCommand
    sudo service mapr-warden start
    ```

    Once you do so, your cluster will re-create the Splice Machine schema, and the command line interface will once again be available after a minute or so.

9.  Restart HBase

    Run this command to restart hbase:

    ``` AppCommand
    ~/splice-installer-mapr4.0/start-hbase.sh
    ```

[]()Cleaning Your Database in the Standalone Version[]()
--------------------------------------------------------

Follow these steps to clean your database if you're using the Standalone version of Splice Machine:

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
    $ ./bin/clean.sh
    $ ./bin/start-splice.sh
    ```

 


