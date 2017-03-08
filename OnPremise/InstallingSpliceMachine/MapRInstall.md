[Open topic with navigation](../../index.html#OnPremise/InstallingSpliceMachine/MapRInstall.html)

[]()Installing and Configuring Splice Machine for MapR
======================================================

This topic describes installing and configuring Splice Machine on a MapR-managed cluster. Follow these steps:

1.  [Verify Prerequisites](#Verify)
2.  [Download and Install Splice Machine](#Install)
3.  [Configure Cluster Services](#Configur)
4.  [Stop Cluster Services](#Stop)
5.  [Restart Cluster Services](#StartCluster)
6.  [Create the Splice Machine Event Log Directory](#CreateLogDir)
7.  Make any needed [Optional Configuration Modifications](#Optional)
8.  [Verify your Splice Machine Installation](#Run)

<span class="noteEnterpriseNote">MapR Secure Clusters Only Work with the Enterprise Edition of Splice Machine</span>

MapR secure clusters do not support the Community Edition of Splice Machine. You can check this by:

1.  Open the HBase Configuration page
2.  Search the XML for the <span class="CodeFont">hbase.security.authentication</span> setting
3.  If the setting value is anything other than <span class="CodeFont">simple</span>, you need the <span class="ItalicFont">Enterprise</span> edition of Splice Machine.

To read more about the additional features available in the Enterprise Edition, see our [Splice Machine Editions](../GettingStarted/SpliceEditions.html) page. To obtain a license for the Splice Machine <span class="ItalicFont">Enterprise Edition</span>, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

[]()Verify Prerequisites
------------------------

Before starting your Splice Machine installation, please make sure that your cluster contains the prerequisite software components:

-   A cluster running MapR with MapR-FS
-   HBase installed
-   YARN installed
-   ZooKeeper installed
-   The latest <span class="CodeFont">mapr-patch</span> should be installed to bring in all MapR-supplied platform patches, before proceeding with your Splice Machine installation.
-   The MapR Ecosystem Package (MEP) should be installed on all cluster nodes, before proceeding with your Splice Machine installation.
-   Ensure Spark services are <span class="BoldFont">NOT</span> installed; Splice Machine cannot currently coexist with Spark 1.x on a cluster:
    -   If <span class="CodeFont">MEP version 1.x</span> is in use, you must remove the <span class="CodeFont">Spark 1.x</span> packages from your cluster, as described below, in [Removing Spark Packages from Your Cluster.](#Removing)
    -   MEP version 2.0 bundles Spark 2.0, and will not cause conflicts with Splice Machine.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The specific versions of these components that you need depend on your operating environment, and are called out in detail in the [Requirements](../GettingStarted/Requirements.html) topic of our <span class="ItalicFont">Getting Started Guide</span>.

### []()Removing Spark Packages from Your Cluster

To remove Spark packages from your cluster and update your configuration, follow these steps

1.  If you're running a Debian/Ubuntu-based Linux distribution:

    ``` ShellCommand
    dpkg -l | awk '/ii.*mapr-spark/{print $2}' | xargs sudo apt-get purge
    ```

    If you're running on a RHEL/CentOS-based Linux distribution:

    ``` ShellCommand
    rpm -qa \*mapr-spark\* | xargs sudo yum -y erase
    ```

2.  Reconfigure node services in your cluster:

    ``` ShellCommand
    sudo /opt/mapr/server/configure.sh -R
    ```

[]()Download and Install Splice Machine
---------------------------------------

Perform the following steps <span class="important">on each node</span> in your cluster:

1.  Contact Splice Machine for your installer

    You'll need to get the URL of your Splice Machine installer (gzip) package; the actual URL you use will depend on which Splice Machine version you're installing and which version of HDP you are using. Here are typical URLs for Splice Machine Release <span class="BasicVariablesSpliceReleaseVersion">2.5</span>:

    | HDP Version                                                  | Installer Package                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
    |--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | <span class="InstallerVersionsMAPR-R1Name">MapR 5.1.0</span> | <span class="InstallerVersionsAWSS3Bucket">https://s3.amazonaws.com/splice-releases</span>/<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>/<span class="InstallerVersionsAWSInstallerPart">cluster/installer</span>/<span class="InstallerVersionsMAPR-R1">mapr5.1.0</span>/SPLICEMACHINE-<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>.<span class="InstallerVersionsMAPR-R1">mapr5.1.0</span>.<span class="InstallerVersionsSpliceReleaseGZ">p0.226.tar.gz</span> |
    | <span class="InstallerVersionsMAPR-R2Name">MapR 5.2.0</span> | <span class="InstallerVersionsAWSS3Bucket">https://s3.amazonaws.com/splice-releases</span>/<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>/<span class="InstallerVersionsAWSInstallerPart">cluster/installer</span>/<span class="InstallerVersionsMAPR-R2">mapr5.2.0</span>/SPLICEMACHINE-<span class="InstallerVersionsCurrentRelease">2.5.0.1707</span>.<span class="InstallerVersionsHDP-R2">hdp2.5.0</span>.<span class="InstallerVersionsSpliceReleaseGZ">p0.226.tar.gz</span>   |

    To be sure that you have the latest URL, please check [the Splice Machine Community site](https://community.splicemachine.com/) or contact your Splice Machine representative.

2.  Create the <span class="CodeFont">splice</span> installation directory:

    ``` ShellCommand
    mkdir -p /opt/splice
    ```

3.  Download the Splice Machine package into the <span class="CodeFont">splice</span> directory on the node. For example:

    ``` ShellCommand
    cd /opt/splice
    curl -O 'https://s3.amazonaws.com/splice-releases/2.5.0.1707/cluster/installer/mapr5.2.0/SPLICEMACHINE-2.5.0.1707.mapr5.2.0.p0.226.tar.gz'
    ```

4.  Extract the Splice Machine package:

    ``` ShellCommand
    tar -xf SPLICEMACHINE-2.5.0.1707.mapr5.2.0.p0.226.tar.gz
    ```

5.  Run our script as <span class="ItalicFont">root</span> user <span class="important">on each node</span> in your cluster to add symbolic links to the set up the Splice Machine jar and to script symbolic links:

    Issue this command on each node in your cluster:

    ``` ShellCommand
    sudo bash /opt/splice/default/scripts/install-splice-symlinks.sh
    ```

6.  Create a symbolic link. For example:

    ``` ShellCommand
    ln -sf SPLICEMACHINE-2.5.0.1707.mapr5.2.0.p0.226 default
    ```

7.  Add the Splice Machine Spark jar to the node manager classpath. For example:

    ``` ShellCommand
    cd /opt/mapr/hadoop/hadoop-2.7.0/share/hadoop/yarn/
    ln -sf /opt/splice/default/lib/spark-assembly-hadoop2.7.0-mapr-1602-1.6.2.jar spark-assembly-hadoop2.7.0-mapr-1602-1.6.2.jar
    ```

[]()Configure Cluster Services
------------------------------

The scripts used in this section all assume that password-less <span class="ShellCommand">ssh </span>and password-less <span class="ShellCommand">sudo </span>are enabled across all cluster nodes. These scripts are designed to be run on the CLDB node in a cluster with only one CLDB node. If your cluster has multiple CLDB nodes, do not run these script; you need to change configuration settings manually <span class="important">on each node</span> in the cluster. To do so, refer to the <span class="CodeFont">\*.patch</span> files in the <span class="CodeFont">/opt/splice/default/conf</span> directory.

If you're running on a cluster with a single CLDB node, follow these steps:

1.  Tighten the ephemeral port range so HBase doesn't bump into it:

    ``` ShellCommand
    cd /opt/splice/default/scripts
    ./install-sysctl-conf.sh
    ```

2.  Update <span class="CodeFont">hbase-site.xml</span>:

    ``` ShellCommand
    cd /opt/splice/default/scripts
    ./install-hbase-site-xml.sh
    ```

3.  Update <span class="CodeFont">hbase-env.sh</span>:

    ``` ShellCommand
    cd /opt/splice/default/scripts
    ./install-hbase-env-sh.sh
    ```

4.  Update <span class="CodeFont">yarn-site.xml</span>:

    ``` ShellCommand
    cd /opt/splice/default/scripts
    ./install-yarn-site-xml.sh
    ```

5.  Update <span class="CodeFont">warden.conf</span>:

    ``` ShellCommand
    cd /opt/splice/default/scripts
    ./install-warden-conf.sh
    ```

6.  Update <span class="CodeFont">zoo.cfg</span>:

    ``` ShellCommand
    cd /opt/splice/default/scripts
    ./install-zookeeper-conf.sh
    ```

[]()Stop Cluster Services
-------------------------

You need to stop all cluster services to continue with installing Splice Machine. Run the following commands as <span class="CodeFont">root</span> user <span class="important">on each node</span> in your cluster

``` ShellCommand
sudo service mapr-warden stop
sudo service mapr-zookeeper stop
```

[]()Restart Cluster Services
----------------------------

Once you've completed the configuration steps described above, start services on your cluster; run the following commands <span class="important">on each node</span> in your cluster:

``` ShellCommand
sudo service mapr-zookeeper start
sudo service mapr-warden start
```

[]()Create the Splice Machine Event Log Directory
-------------------------------------------------

Create the Splice Machine event log directory by executing the following commands on a single cluster node while MapR is up and running:

``` ShellCommand
sudo -su mapr hadoop fs -mkdir -p /user/splice/history
sudo -su mapr hadoop fs -chown -R mapr:mapr /user/splice
sudo -su mapr hadoop fs -chmod 1777 /user/splice/history
```

[]()Optional Configuration Modifications
----------------------------------------

There are a few configuration modifications you might want to make:

-   [Modify the Authentication Mechanism](#Modify) if you want to authenticate users with something other than the default <span class="ItalicFont">native authentication</span> mechanism.
-   [Adjust the Replication Factor](#Adjust) if you have a small cluster and need to improve resource usage or performance.

### []()Modify the Authentication Mechanism

Splice Machine installs with Native authentication configured; native authentication uses the <span class="CodeFont">sys.sysusers</span> table in the <span class="CodeFont">splice</span> schema for configuring user names and passwords.

You can disable authentication or change the authentication mechanism that Splice Machine uses to LDAP by following the simple instructions in <a href="../../Shared/CmdLineReference/Intro.CmdLineReference.html" class="WithinBook">Command Line (splice&gt;) Reference</a>

### []()Adjust the Replication Factor

The default namespace replication factor for Splice Machine is <span class="PlatformVariablesMapRDefaultReplication">3</span>. If you're running a small cluster you may want to adjust the replication down to improve resource and performance drag. To do so in MapR, use the following command:

``` ShellCommand
maprcli volume modify -nsreplication <value>
```

For more information, see the MapR documentation site, [doc.mapr.com](http://doc.mapr.com/ "MapR documentation site").

[]()Verify your Splice Machine Installation
-------------------------------------------

Now start using the Splice Machine command line interpreter, which is referred to as <span class="ItalicFont">the splice prompt</span> or simply <span class="AppCommand">splice&gt;</span> by launching the <span class="CodeFont">sqlshell.sh</span> script on any node in your cluster that is running an HBase region server.

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

List available commands
``` AppCommandCell
splice> help;
```

Exit the command line interpreter
``` AppCommandCell
splice> exit;
```

<span class="BoldFont">Make sure you end each command with a semicolon</span> (<span class="CodeFont">;</span>), followed by the <span class="ItalicFont">Enter</span> key or <span class="ItalicFont">Return</span> key
See the [Command Line (splice&gt;) Reference](../../Shared/CmdLineReference/Intro.CmdLineReference.html) section of our <span class="ItalicFont">Developer's Guide</span> for information about our commands and command syntax.

 


