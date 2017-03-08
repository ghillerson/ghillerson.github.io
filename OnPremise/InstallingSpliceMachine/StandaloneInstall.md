[Open topic with navigation](../../index.html#OnPremise/InstallingSpliceMachine/StandaloneInstall.html)

[]()Installing the Standalone Version of Splice Machine[]()
===========================================================

This topic walks you through downloading, installing, and getting started with using the standalone version of Splice Machine.

About the Standalone Version
----------------------------

The standalone version of Splice Machine runs on a single computer, rather than on a cluster; it is intended to allow you to get your feet wet with Splice Machine. The standalone version installs quickly on your MacOS, Linux, or CentOS computer, and enables rapid access to Splice Machine's capabilities. It's an excellent way to experiment with Splice Machine with a reasonably small amount of data.

Note that many of our customers also use the standalone version of Splice Machine for ongoing development work. For example, if your engineers want to create stored procedures to optimize aspects of your database, they can develop and debug those procedures on the standalone version before deploying them to your cluster.

This topic will walk you through installing the standalone version, in these sections:

-   [Install Splice Machine](#Installi) walks you through installing Splice Machine on your computer.
-   [Start Using Splice Machine](#Start) shows you how to start Splice Machine and use the <span class="AppCommand">splice&gt;</span> command line.
-   [Import and Query the Sample Data](#Import) helps you to import our sample database and then start making queries against the sample data. This is an optional but recommended step.

[]()Install Splice Machine
--------------------------

This topic describes how to download and launch the <span class="ItalicFont">Standalone</span> version of Splice Machine using our command line installer. Follow these steps:

-   [1. Prepare for Installation](#1.)
-   [2. Install the Java JDK if Necessary](#2.)
-   [3. Download Splice Machine](#3.)
-   [4. Install and Start Splice Machine](#4.)

### []()1. Prepare for Installation

If you already have Hadoop installed on your computer, stop any Hadoop processes that are running. If you don't have Hadoop, the Splice Machine installer will automatically install the Hadoop packages required for our software.

You should also make sure that your hardware and software meet our basic requirements, which are described in the introduction to this [Splice Machine Installation Guide](Intro.InstallationGuide.html).

#### []()Additional Steps for CentOS/RHEL Installations

If you are using the standalone version of Splice Machine with CentOS or RHEL, you need address a few configuration issues to allow Splice Machine to work. Follow these steps:

1.  Install wget

    CentOS and RHEL use <span class="CodeFont">yum</span> instead of <span class="CodeFont">apt-get</span> to install software packages. By default, it does not have <span class="CodeFont">wget</span> installed. For Splice Machine to work properly, you need to install <span class="CodeFont">wget</span> with the following command:

    ``` ShellCommand
    yum install wget
    ```

2.  Change the default security settings

    The default security settings interfere with Cloudera Manager, and in some circumstances, even with Splice Machine. You need to change security to <span class="ShellCommand">SELINUX=disabled</span> in the following file :

    ``` ShellCommand
    /etc/selinux/config
    ```

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>After making this change, you must reboot before you use Splice Machine.

3.  Configure the firewall

    You need to turn off the CentOS/RHEL firewall, using the following command sequence:

    ``` ShellCommand
    /etc/init.d/iptables stop
    chkconfig iptables off
    ```

4.  Set the data files directory location

    The HDFS file system files are set up on CentOS/RHEL using the <span class="CodeFont">hfds</span> user. An important note is that CentOS/RHEL does not grant the <span class="CodeFont">hdfs</span> user access to the <span class="CodeFont">/root</span> directory,

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>CentOS and RHEL do not grant the <span class="CodeFont">hdfs</span> user access to the <span class="CodeFont">/root</span> directory, which means you must make sure that any local files you want to access from HDFS are in directories that the <span class="CodeFont">hdfs</span> user can access.

    The implication is that you need to store your data files in a directory that the <span class="CodeFont">hdfs</span> user can access. We recommend storing data files that you want to access as <span class="CodeFont">hdfs</span> in the <span class="CodeFont">/tmp</span>directory. For example, the following Hadoop shell command is executed as user <span class="CodeFont">hdfs</span>, and thus the source file must be in a directory that hdfs can access:

    ``` ShellCommand
    sudo -su hdfs hadoop copyFromLocal /tmp/datafile.csv /data
    ```

### []()2. Install the Java JDK if Necessary

You need to have Java installed on your computer;

Splice Machine supports the following versions of the Java JDK:

-   Oracle JDK 1.8, update 60 or higher

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>We recommend that you do not use JDK 1.8.0\_40

Splice Machine does not test our releases with OpenJDK, so we recommend against using it.

Install the Java Development Kit (JDK) by following the instructions for your operating system:

-   [Install Java JDK For MacOS](#Install2)
-   [Install Java JDK For Ubuntu Linux](#Install3)
-   [Install Java JDK For CentOS or RHEL](#Install4)

#### []()Install Java JDK For MacOS

Follow the MacOS Java JDK installation instructions on the [Oracle web site](http://docs.oracle.com/javase/7/docs/webnotes/install/mac/mac-jdk.html "Link to Oracle JDK 7 installation instructions for Mac OS X").

#### []()Install Java JDK For Ubuntu Linux

1.  Update packages:

    Update your list of sources and your database of packages:

    ``` ShellCommand
    sudo add-apt-repository ppa:webupd8team/java
    sudo apt-get update
    ```

2.  Download and install:

    Download and install the java packages; for example:

    ``` ShellCommand
    sudo apt-get install oracle-java7-installer
    sudo apt-get install oracle-java7-set-default
    ```

3.  Create a soft link for YARN support:

    ``` ShellCommand
    sudo ln -s /usr/bin/java /bin/java
    ```

#### []()Install Java JDK For CentOS or RHEL

1.  Download packages

    Download the java package; for example:

    ``` ShellCommand
    wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie"
       http://download.oracle.com/otn-pub/java/jdk/7u67-b01/jdk-7u67-linux-x64.rpm
    ```

2.  Download and install

    Download and install the java packages; for example:

    ``` ShellCommand
    sudo rpm -Uhv jdk-7u67-linux-x64.rpm
    ```

### []()3. Download Splice Machine

Visit our [standalone download page](https://www.splicemachine.com/get-started/download/ "Click to access the Splice Machine standalone download page") to download the installer package tarball (<span class="CodeFont">.gz</span> file).

### []()4. Install and Start Splice Machine

Use the command line to install and start Splice Machine:

1.  Navigate to the directory on your computer in which you want to install Splice Machine

    You should only install in a directory whose name does not contain spaces, because some scripts will not operate correctly if the working directory has spaces in its name.

2.  Move the downloaded tarball:

    Move the installer package <span class="CodeFont">.gz</span> file you downloaded into the directory in which you are installing Splice Machine.

3.  Install Splice Machine:

    Unpack the tarball <span class="CodeFont">gz</span> file that you downloaded:

    ``` ShellCommand
    tar -xzf splice-releases/2.5.0.1707/standalone
    ```

    This creates a <span class="CodeFont">splicemachine</span> subdirectory and installs Splice Machine software in it.

4.  Start Using Splice Machine

    Start Splice Machine and run a few commands to verify your installation, as described in the next section, [Start Using Splice Machine](#Start).

[]()Start Using Splice Machine
------------------------------

Start Splice Machine on your computer and run a few commands to verify the installation:

1.  Make your install directory the current directory

    ``` ShellCommand
    cd splicemachine
    ```

2.  Run the Splice Machine start-up script

    ``` ShellCommand
    ./bin/start-splice.sh
    ```

    Initialization of the database may take a couple minutes. It is ready for use when you see this message:

    ``` ShellCommand
    Splice Server is ready
    ```

3.  Start using the Splice Machine command line interpreter by launching the <span class="CodeFont">sqlshell.sh</span> script:

    ``` ShellCommand
    ./bin/sqlshell.sh
    ```

    Once you have launched the command line interpreter (the <span class="AppCommand">splice&gt;</span> prompt), we recommend verifying that all is well by running a few sample commands. Here are a few you can try:

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="BoldFont">Make sure you end each command with a semicolon</span> (<span class="CodeFont">;</span>), followed by the <span class="ItalicFont">Enter</span> key or <span class="ItalicFont">Return</span> key.

    Operation

    Command to perform operation

    Show defined tables

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

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>While the database is running, logging information is written to the <span class="CodeFont">splice.log</span> file, which is found in the <span class="CodeFont">splicemachine</span> directory.

    Splice Machine displays the result of each statement. For example:

    ``` AppCommand
    7 rows inserted/updated/deleted
    ```

    If a statement doesn't add, update, or delete data, you'll see this message:

    ``` AppCommand
    0 rows inserted/updated/deleted
    ```

[]()Import and Query the Sample Data
------------------------------------

The Splice Machine installer package includes sample data that you can import into your database, so you can get used to working with your new database. We recommend that you follow the steps in this topic to import this sample data, and then run a few test queries against it to verify your installation.

The sample data included in your installer package requires about 30 MB in compressed format. Importing the sample data creates three tables, each of which contains one million records:

<table style="width:70%;">
<colgroup>
<col width="0%" />
<col width="70%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Table</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span class="CodeFont">T_HEADER</span></td>
<td align="left">Standard <span class="ItalicFont">headers</span> from a transaction system</td>
</tr>
<tr class="even">
<td align="left"><span class="CodeFont">T_DETAIL</span></td>
<td align="left">Standard <span class="ItalicFont">detail</span> records from a transaction system</td>
</tr>
<tr class="odd">
<td align="left"><span class="CodeFont">CUSTOMERS</span></td>
<td align="left">A list of target <span class="ItalicFont">customers</span></td>
</tr>
</tbody>
</table>

### []()Import the Data

Follow these steps to import the sample data into your Splice Machine database:

1.  Start the command line interpreter

    You can use the Splice Machine command line interpreter (CLI), or <span class="AppCommand">splice&gt;</span> prompt, to work directly with your database. If you're using the cluster version of Splice Machine, you can access the <span class="AppCommand">splice&gt;</span> prompt by entering this shell command on any node on which it is available:

    ``` ShellCommand
    ./sqlshell.sh
    ```

    If you're using the standalone version of Splice Machine, use these steps to access the <span class="AppCommand">splice&gt;</span> prompt:

    ``` ShellCommand
    cd <your.splicemachine-directory>
    ./bin/sqlshell.sh
    ```

2.  Modify the script that loads the data to use your path:

    Before running the <span class="AppCommand">loadall.sql</span> script, you must change the file path used in the script.

    There are calls to <span class="CodeFont">SYSCS\_UTIL.IMPORT\_DATA</span> near the bottom of the script. Change the file path parameter in each of these calls to use the absolute path to your Splice Machine <span class="CodeFont">demodata</span> directory:

    ``` ShellCommand
    call SYSCS_UTIL.IMPORT_DATA('SPLICE', 'T_HEADER',  null, '<yourPath>/demodata/data/theader.csv.gz', ...;
    call SYSCS_UTIL.IMPORT_DATA('SPLICE', 'T_DETAIL',  null, '<yourPath>/demodata/data/tdetail.csv.gz', ...;
    call SYSCS_UTIL.IMPORT_DATA('SPLICE', 'CUSTOMERS', null, '<yourPath>/demodata/data/customers.csv.gz', ...;
    ```

    Make sure you use the absolute (versus relative) path. For example:

    ``` ShellCommand
    call SYSCS_UTIL.IMPORT_DATA('SPLICE', 'T_HEADER',  null, '/Users/myName/mySplice/demodata/data/theader.csv.gz', ...;
    call SYSCS_UTIL.IMPORT_DATA('SPLICE', 'T_DETAIL',  null, '/Users/myName/mySplice/demodata/data/tdetail.csv.gz', ...;
    call SYSCS_UTIL.IMPORT_DATA('SPLICE', 'CUSTOMERS', null, '/Users/myName/mySplice/demodata/data/customers.csv.gz',...;
    ```

3.  Run the modify script to loads the data:

    From the <span class="AppCommand">splice&gt;</span> prompt, <span class="ItalicFont">run</span> the file that will load the data, using single quotes around the path/filename (and remember to include the semicolon at the end):

    ``` ShellCommand
    splice> run 'demodata/sql/loadall.sql';
    ```

4.  Wait for the script to finish

    If your database is not currently running, start it up and launch the command line interpreter (<span class="AppCommand">splice&gt;</span> prompt) by issuing this command in your terminal window:

    ``` ShellCommand
    ./bin/sqlshell.sh
    ```

    The loading process can take several minutes: the <span class="CodeFont">loadall.sql</span> file creates the schema, loads the data, and creates indexes for the tables.

    <span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>While the database is running, logging information is written to the <span class="CodeFont">splice.log</span> file, which is found in the <span class="CodeFont">splicemachine</span> directory.

    When you again see the <span class="AppCommand">splice&gt;</span> prompt, the sample data is ready to use. We recommend running the sample queries in the next section to get a feel for using Splice Machine and the sample data.

### []()Run Sample Queries

After you have imported the sample data, you can use the command line interpreter to run the sample queries on this page to get some experience with using Splice Machine.

You can simply copy the select command from each of the samples below to your clipboard. Then paste from the clipboard at the <span class="AppCommand">splice&gt;</span> prompt and press the <span class="ItalicFont">Enter</span> key or <span class="ItalicFont">Return</span> key to submit the query.

#### Example of Selecting a Subset

You can use the following query to select the customer IDs from a subset of the transaction detail (<span class="CodeFont">T\_DETAIL</span>) table, based on transaction date and category ID.

``` Example
select customer_master_id
   from T_DETAIL d
   where TRANSACTION_DT >= DATE('2010-01-01')
      and TRANSACTION_DT <= DATE('2013-12-31')
      AND ORIGINAL_SKU_CATEGORY_ID >= 44427
      and original_sku_category_id <= 44431;
```

#### Example of Selecting With a Join

You can use the following to query a join of the <span class="CodeFont">T\_HEADER</span> and <span class="CodeFont">CUSTOMERS</span> tables.

``` Example
select t.transaction_header_key, t.transaction_dt, t.store_nbr,
       t.geocapture_flg, t.exchange_rate_percent 
   from T_HEADER t, CUSTOMERS c
   where c.customer_master_id=t.customer_master_id
   and t.customer_master_id > 14000
   and t.customer_master_id < 15000;
```

### Troubleshooting Transaction Exceptions on MacOS

If you're running transactions in the standalone version of Splice Machine on MacOS, you may run into an exception caused by the clock having moved backwards. This happens only rarely, and is due to the fact that OS X has its own time-maintenance daemon that can (rarely) cause the clock to move backwards, which causes a transaction exception.

When this happens, you'll see an exception messages like the following:

``` AppCommand
SQLSTATE: XJ001Java exception: 'java.io.IOException: java.lang.IllegalStateException: Unable to obtain timestamp, clock moved backwards
```

To correct the problem, simply re-run the query or statement that generated the exception.

 


