[Open topic with navigation](../../index.html#OnPremise/InstallingSpliceMachine/HDPInstall.html)

[]()Installing and Configuring Splice Machine for Hortonworks HDP
=================================================================

This topic describes installing and configuring Splice Machine on a Hortonworks Ambari-managed cluster. Follow these steps:

1.  [Verify Prerequisites](#Verify)
2.  [Download and Install Splice Machine](#Install)
3.  [Stop Hadoop Services](#Stop)
4.  [Configure Hadoop Services](#Configur8)
5.  [Start Any Additional Services](#Start)
6.  Make any needed [Optional Configuration Modifications](#Optional)
7.  [Verify your Splice Machine Installation](#Run)

[]()Verify Prerequisites
------------------------

Before starting your Splice Machine installation, please make sure that your cluster contains the prerequisite software components:

-   A cluster running HDP
-   Ambari installed and configured for HDP
-   HBase installed
-   HDFS installed
-   YARN installed
-   ZooKeeper installed
-   Ensure that Spark services are <span class="BoldFont">NOT</span> installed on your cluster; Splice Machine cannot currently coexist with Spark 1.x on a cluster.
-   Ensure that Phoenix services are <span class="BoldFont">NOT</span> installed on your cluster, as they interfere with Splice Machine HBase settings.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The specific versions of these components that you need depend on your operating environment, and are called out in detail in the [Requirements](../GettingStarted/Requirements.html) topic of our <span class="ItalicFont">Getting Started Guide</span>.

[]()Download and Install Splice Machine
---------------------------------------

Perform the following steps <span class="important">on each node</span> in your cluster:

1.  Contact Splice Machine for your installer

    You'll need to get the URL of your Splice Machine installer (gzip) package; the actual URL you use will depend on which Splice Machine version you're installing and which version of HDP you are using. Here are typical URLs for Splice Machine Release <span class="BasicVariablesSpliceReleaseVersion">2.5</span>:

    | HDP Version                                                | Installer Package                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
    |------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | <span class="InstallerVersionsHDP-R1Name">HDP 2.4.2</span> | <span class="InstallerVersionsAWSS3Bucket">https://s3.amazonaws.com/splice-releases</span>/<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>/<span class="InstallerVersionsAWSInstallerPart">cluster/installer</span>/<span class="InstallerVersionsHDP-R1">hdp2.4.2</span>/SPLICEMACHINE-<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>.<span class="InstallerVersionsHDP-R1">hdp2.4.2</span>.<span class="InstallerVersionsSpliceReleaseGZ">p0.226.tar.gz</span> |
    | <span class="InstallerVersionsHDP-R2Name">HDP 2.5.0</span> | <span class="InstallerVersionsAWSS3Bucket">https://s3.amazonaws.com/splice-releases</span>/<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>/<span class="InstallerVersionsAWSInstallerPart">cluster/installer</span>/<span class="InstallerVersionsHDP-R2">hdp2.5.0</span>/SPLICEMACHINE-<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>.<span class="InstallerVersionsHDP-R2">hdp2.5.0</span>.<span class="InstallerVersionsSpliceReleaseGZ">p0.226.tar.gz</span> |

    To be sure that you have the latest URL, please check [the Splice Machine Community site](https://community.splicemachine.com/) or contact your Splice Machine representative.

2.  Create the <span class="CodeFont">splice</span> installation directory:

    ``` ShellCommandCell
    sudo mkdir -p /opt/splice
    ```

3.  Download the Splice Machine package into the <span class="CodeFont">splice</span> directory on the node. For example:

    ``` ShellCommandCell
    sudo curl 'https://s3.amazonaws.com/splice-releases/2.5.0.1707/cluster/installer/hdp2.5.0/SPLICEMACHINE-2.5.0.1707.hdp2.5.0.p0.226.tar.gz' -o /opt/splice/SPLICEMACHINE-2.5.0.1707.hdp2.5.0.p0.226.tar.gz
    ```

4.  Extract the Splice Machine package:

    ``` ShellCommandCell
    sudo tar -xf SPLICEMACHINE-2.5.0.1707.hdp2.5.0.p0.226.tar.gz --directory /opt/splice
    ```

5.  Run our script as <span class="ItalicFont">root</span> user <span class="important">on each node</span> in your cluster to add symbolic links to set up Splice Machine jar script symbolic links

    Issue this command <span class="important">on each node</span> in your cluster:

    ``` AppCommand
    sudo /opt/splice/default/scripts/install-splice-symlinks.sh
    ```

[]()Stop Hadoop Services
------------------------

As a first step, we stop cluster services to allow our installer to make changes that require the cluster to be temporarily inactive.

1.  Access the Ambari Home Screen

2.  Click the <span class="AppCommand">Actions</span> drop-down, and then click the <span class="AppCommand">Stop All</span> button.

[]()Configure Hadoop Services
-----------------------------

Now it's time to make a few modifications in the Hadoop services configurations:

-   <a href="#Configur4" class="MCXref xref">Configure and Restart ZooKeeper</a>
-   <a href="#Configur5" class="MCXref xref">Configure and Restart HDFS</a>
-   <a href="#Configur2" class="MCXref xref">Configure and Restart YARN</a>
-   <a href="#Configur" class="MCXref xref">Configure MapReduce2</a>
-   <a href="#Configur3" class="MCXref xref">Configure and Restart HBASE</a>

### []()[]()Configure and Restart ZooKeeper

To edit the ZooKeeper configuration, select the <span class="AppCommand">Services</span> tab at the top of the Ambari dashboard screen, then click <span class="AppCommand">ZooKeeper</span> in the Ambari in the left pane of the screen.

1.  Select the <span class="AppCommand">Configs</span> tab to configure ZooKeeper

2.  Make configuration changes:

    Scroll down to where you see <span class="ItalicFont">Custom zoo.cfg</span> and click <span class="AppCommand">Add Property</span> to add the <span class="CodeFont">maxClientCnxns</span> property and then again to add the <span class="CodeFont">maxSessionTimeout</span> property, with these values:

    ``` AppCommand
    maxClientCnxns=0
    maxSessionTimeout=120000
    ```

3.  Save Changes

    Click the <span class="AppCommand">Save</span> button to save your changes. You'll be prompted to optionally add a note such as <span class="CodeFont">Updated ZooKeeper configuration for Splice Machine</span>. Click <span class="AppCommand">Save</span> again.

4.  Start ZooKeeper

    After you save your changes, you'll land back on the ZooKeeper Service <span class="AppCommand">Configs</span> tab in Ambari.

    Open the <span class="AppCommand">Service Actions</span> drop-down in the upper-right corner and select the <span class="AppCommand">Start</span> action to start ZooKeeper. Wait for the restart to complete.

### []()[]()Configure and Restart HDFS

To edit the HDFS configuration, select the <span class="AppCommand">Services</span> tab at the top of the Ambari dashboard screen, then click <span class="AppCommand">HDFS</span> in the Ambari in the left pane of the screen. Finally, click the <span class="AppCommand">Configs</span> tab.

1.  Edit the HDFS configuration as follows:

    |                                 |                                                                       |
    |---------------------------------|-----------------------------------------------------------------------|
    | NameNode Java heap size         | 4 GB                                                                  |
    | DataNode maximum Java heap size | 2 GB                                                                  |
    | Block replication               | 2 <span class="bodyFont">(for clusters with less than 8 nodes)</span> 
                                                                                                              
                                       3 <span class="bodyFont">(for clusters with 8 or more nodes)</span>    |

2.  Add a new property:

    Click <span class="AppCommand">Add Property</span>... under <span class="AppCommand">Custom hdfs-site</span>, and add the following property:

    ``` AppCommand
    dfs.datanode.handler.count=20
    ```

3.  Save Changes

    Click the <span class="AppCommand">Save</span> button to save your changes. You'll be prompted to optionally add a note such as <span class="CodeFont">Updated HDFS configuration for Splice Machine</span>. Click <span class="AppCommand">Save</span> again.

4.  Start HDFS

    After you save your changes, you'll land back on the <span class="AppCommand">HDFS Service Configs</span> tab in Ambari.

    Open the <span class="AppCommand">Service Actions</span> drop-down in the upper-right corner and select the <span class="AppCommand">Start</span> action to start HDFS. Wait for the restart to complete.

5.  Create directories for hbase user and the Splice Machine YARN application:

    Use your terminal window to create these directories:

    ``` ShellCommand
    sudo -iu hdfs hadoop fs -mkdir -p hdfs:///user/hbase hdfs:///user/splice/history
    sudo -iu hdfs hadoop fs -chown -R hbase:hbase hdfs:///user/hbase hdfs:///user/splice
    sudo -iu hdfs hadoop fs -chmod 1777 hdfs:///user/splice hdfs:///user/splice/history
    ```

### []()Configure and Restart YARN

To edit the YARN configuration, select the <span class="AppCommand">Services</span> tab at the top of the Ambari dashboard screen, then click <span class="AppCommand">YARN</span> in the Ambari in the left pane of the screen. Finally, click the <span class="AppCommand">Configs</span> tab.

1.  Update these other configuration values:

    | Setting                                                 | New Value                                        |
    |---------------------------------------------------------|--------------------------------------------------|
    | yarn.application.classpath                              |                                                  |
    | yarn.nodemanager.aux-services.spark2\_shuffle.classpath | /opt/splice/default/lib/\*                       |
    | yarn.nodemanager.aux-services.spark\_shuffle.classpath  | /opt/splice/default/lib/\*                       |
    | yarn.nodemanager.aux-services.spark2\_shuffle.class     | org.apache.spark.network.yarn.YarnShuffleService |
    | yarn.nodemanager.delete.debug-delay-sec                 | 86400                                            |
    | Memory allocated for all YARN containers on a node      | 30 GB (based on node specs)                      |
    | Minimum Container Size (Memory)                         | 1 GB (based on node specs)                       |
    | Minimum Container Size (Memory)                         | 30 GB (based on node specs)                      |

2.  Save Changes

    Click the <span class="AppCommand">Save</span> button to save your changes. You'll be prompted to optionally add a note such as <span class="CodeFont">Updated YARN configuration for Splice Machine</span>. Click <span class="AppCommand">Save</span> again.

3.  Start YARN

    After you save your changes, you'll land back on the <span class="AppCommand">YARN Service Configs</span> tab in Ambari.

    Open the <span class="AppCommand">Service Actions</span> drop-down in the upper-right corner and select the <span class="AppCommand">Start</span> action to start YARN. Wait for the restart to complete.

### []()Configure MapReduce2

Ambari automatically sets these values for you:

-   Map Memory
-   Reduce Memory
-   Sort Allocation Memory
-   AppMaster Memory
-   MR Map Java Heap Size
-   MR Reduce Java Heap Size

You do, however, need to make a few property changes for this service. To edit the MapReduce2 configuration, select the <span class="AppCommand">Services</span> tab at the top of the Ambari dashboard screen, then click <span class="AppCommand">MapReduce2</span> in the Ambari in the left pane of the screen. Finally, click the <span class="AppCommand">Configs</span> tab.

1.  Select the <span class="AppCommand">Configs</span> tab to configure MapReduce2.

2.  Update property values

    You need to replace <span class="AppFontCustCode">${hdp.version}</span> with the actual HDP version number you are using in these property values:

    -   mapreduce.admin.map.child.java.opts
    -   mapreduce.admin.reduce.child.java.opts
    -   mapreduce.admin.user.env
    -   mapreduce.application.classpath
    -   mapreduce.application.framework.path
    -   yarn.app.mapreduce.am.admin-command-opts
    -   MR AppMaster Java Heap Size

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>An example of an HDP version number that you would substitute for <span class="AppFontCustCode">${hdp.version}</span> is <span class="CodeFont">2.5.0.0-1245</span>.

3.  Save Changes

    Click the <span class="AppCommand">Save</span> button to save your changes. You'll be prompted to optionally add a note such as <span class="CodeFont">Updated MapReduce2 configuration for Splice Machine</span>. Click <span class="AppCommand">Save</span> again.

4.  Start MapReduce2

    After you save your changes, you'll land back on the MapReduce2 Service <span class="AppCommand">Configs</span> tab in Ambari.

    Open the <span class="AppCommand">Service Actions</span> drop-down in the upper-right corner and select the <span class="AppCommand">Start</span> action to start MapReduce2. Wait for the restart to complete.

### []()Configure and Restart HBASE

To edit the HBASE configuration, click <span class="AppCommand">HBASE</span> in the Cloudera Manager home screen, then click the <span class="AppCommand">Configuration</span> tab and make these changes:

1.  Change the values of these settings

    | Setting                                        | New Value                                                                          |
    |------------------------------------------------|------------------------------------------------------------------------------------|
    | % of RegionServer Allocated to Write Buffer    
     (hbase.regionserver.global.memstore.size)       | 0.25                                                                               |
    | HBase RegionServer Maximum Memory              
      (hbase\_regionserver\_heapsize)                | 24 GB                                                                              |
    | % of RegionServer Allocated to Read Buffers    
      (hfile.block.cache.size)                       | 0.25                                                                               |
    | HBase Master Maximum Memory                    
      (hbase\_master\_heapsize)                      | 5 GB                                                                               |
    | Number of Handlers per RegionServer            
      (hbase.regionserver.handler.count)             | 200                                                                                |
    | HBase RegionServer Meta-Handler Count          | 200                                                                                |
    | HBase RPC Timeout                              | 1200000 (20 minutes)                                                               |
    | Zookeeper Session Timeout                      | 120000 (2 minutes)                                                                 |
    | hbase.coprocessor.master.classes               | com.splicemachine.hbase.SpliceMasterObserver                                       |
    | hbase.coprocessor.region.classes               | <span class="bodyFont">The value of this property is shown below, in Step 2</span> |
    | Maximum Store Files before Minor Compaction    
     (hbase.hstore.compactionThreshold)              | 5                                                                                  |
    | Number of Fetched Rows when Scanning from Disk 
      (hbase.client.scanner.caching)                 | 1000                                                                               |
    | hstore blocking storefiles                     
      (hbase.hstore.blockingStoreFiles)              | 20                                                                                 |
    | Advanced hbase-env                             | <span class="bodyFont">The value of this property is shown below, in Step 3</span> |
    | Custom hbase-site                              | <span class="bodyFont">The value of this is shown below, in Step 4</span>          |

2.  Set the value of the <span class="CodeFont">hbase.coprocessor.region.classes</span> property to the following:

3.  Under <span class="CodeFont">Advanced hbase-env</span>, set the value of <span class="CodeFont">hbase-env template</span> to the following:

4.  In <span class="CodeFont">Custom hbase-site</span> property, add the following properties:

5.  Save Changes

    Click the <span class="AppCommand">Save</span> button to save your changes. You'll be prompted to optionally add a note such as <span class="CodeFont">Updated HDFS configuration for Splice Machine</span>. Click <span class="AppCommand">Save</span> again.

6.  Start HBase

    After you save your changes, you'll land back on the HBase Service <span class="AppCommand">Configs</span> tab in Ambari.

    Open the <span class="AppCommand">Service Actions</span> drop-down in the upper-right corner and select the <span class="AppCommand">Start</span> action to start HBase. Wait for the restart to complete.

[]()Start any Additional Services
---------------------------------

We started this installation by shutting down your cluster services, and then configured and restarted each individual service used by Splice Machine.

If you had any additional services running, such as Ambari Metrics, you need to restart each of those services.

[]()Optional Configuration Modifications
----------------------------------------

There are a few configuration modifications you might want to make:

-   [Modify the Authentication Mechanism](#Modify) if you want to authenticate users with something other than the default <span class="ItalicFont">native authentication</span> mechanism.
-   Adjust the replication factor if you have a small cluster and need to improve resource usage or performance.

### []()Modify the Authentication Mechanism

Splice Machine installs with Native authentication configured; native authentication uses the <span class="CodeFont">sys.sysusers</span> table in the <span class="CodeFont">splice</span> schema for configuring user names and passwords.

You can disable authentication or change the authentication mechanism that Splice Machine uses to LDAP by following the simple instructions in <a href="Authentication.html" class="WithinBook">Configuring Splice Machine Authentication</a>

[]()Verify your Splice Machine Installation
-------------------------------------------

Now start using the Splice Machine command line interpreter, which is referred to as <span class="AppCommand">the splice prompt</span> or simply <span class="AppCommand">splice&gt;</span> by launching the <span class="CodeFont">sqlshell.sh</span> script on any node in your cluster that is running an HBase region server.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The command line interpreter defaults to connecting on port <span class="CodeFont">1527</span> on <span class="CodeFont">localhost</span>, with username <span class="CodeFont">splice</span>, and password <span class="CodeFont">admin</span>. You can override these defaults when starting the interpreter, as described in the [Command Line (splice&gt;) Reference](../../Shared/CmdLineReference/Intro.CmdLineReference.html) topic in our <span class="ItalicFont">Developer's Guide</span>.

Now try entering a few sample commands you can run to verify that everything is working with your Splice Machine installation.

Operation
Command to perform operation
Display tables
``` AppCommandCell
splice> show tables;
```

Create a table
``` AppCommandCell
splice> create table test (i int);
```

Add data to the table
``` AppCommandCell
splice> insert into test values 1,2,3,4,5;
```

Query data in the table
``` AppCommandCell
splice> select * from test;
```

Drop the table
``` AppCommandCell
splice> drop table test;
```

Exit the command line interpreter
``` AppCommandCell
splice> exit;
```

<span class="BoldFont">Make sure you end each command with a semicolon</span> (<span class="CodeFont">;</span>), followed by the <span class="ItalicFont">Enter</span> key or <span class="ItalicFont">Return</span> key
See the [Command Line (splice&gt;) Reference](../../Shared/CmdLineReference/Intro.CmdLineReference.html) section of our <span class="ItalicFont">Developer's Guide</span> for information about our commands and command syntax.

 


