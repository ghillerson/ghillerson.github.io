[Open topic with navigation](../../index.html#OnPremise/Administrators/StartingDatabase.html)

Starting Your Database
======================

-   [Starting Your Splice Machine Database on a Cloudera-Managed Cluster](#StartDBCloudera)
-   [Starting Your Splice Machine Database on a Hortonworks HDP-Managed Cluster](#StartDBHDP)
-   [Starting Your Splice Machine Database on a MapR-Managed Cluster](#StartDBMapR)
-   [Starting Your Splice Machine Database on a Standalone installation](#StartDbStandalone)

[]()[]()Starting Your Splice Machine Database on a Cloudera-Managed Cluster
---------------------------------------------------------------------------

Use the Cloudera Manager to start HBase:

1.  Navigate to the <span class="ItalicFont">Services-&gt;All Services</span> screen in <span class="ItalicFont">Cloudera Manager</span>, and select this action to start <span class="ItalicFont">HBase</span>:

    ``` AppCommand
    Actions -> Start
    ```

[]()[]()Starting Your Splice Machine Database on a Hortonworks HDP--Managed Cluster
-----------------------------------------------------------------------------------

Use the Ambari dashboard to start Splice Machine:

1.  Log in to the Ambari Dashboard by pointing your browser to the publicly visible <span class="HighlightedCode">&lt;hostName&gt;</span> for your master node that is hosting Ambari Server:

    ``` ShellCommand
    http://<hostName>:8080/
    ```

2.  Start cluster services:

    ``` AppCommand
    Action -> Start All
    ```

[]()[]()Starting Your Splice Machine Database on a MapR-Managed Cluster
-----------------------------------------------------------------------

To start Splice Machine, use the MapR Command System (MCS):

1.  Navigate to the node that is running the <span class="CodeFont">mapr-webserver</span> service.
2.  Log into <span class="CodeFont">https://<span class="HighlightedCode">&lt;hostIPAddr&gt;</span>:8443</span>, substituting the correct <span class="HighlightedCode">&lt;hostIPAddr&gt;</span> value. The login credentials are the ones you used when you added the <span class="CodeFont">mapr</span> user during installation.
3.  Start your HBase master
4.  Start all of your Region Servers

[]()Starting Your Database in the Standalone Version[]()
--------------------------------------------------------

Follow these steps to start your database if you're using the Standalone version of Splice Machine:

1.  Change directory to your install directory:

    ``` ShellCommand
    cd splicemachine
    ```

2.  Run the Splice Machine start-up script:

    ``` ShellCommand
    $ ./bin/start-splice.sh
    ```

### Restarting Splice Machine

If you're running the standalone version of Splice Machine on a personal computer that goes into sleep mode, you need to stop and then restart Splice Machine when you wake the computer back up. For example, if you're running Splice Machine on a laptop, and close your laptop, then you'll need to stop and restart Splice Machine when you reopen your laptop.

To stop and restart Splice Machine, follow these steps:

1.  Make sure that you have quit the <span class="AppCommand">splice&gt;</span> command line interpreter:

    ``` AppCommand
    splice> quit;
    ```

2.  Change directory to your install directory:

    ``` ShellCommand
    cd splicemachine
    ```

3.  Run the Splice Machine shut-down script:

    ``` ShellCommand
    $ ./bin/stop-splice.sh
    ```

4.  Run the Splice Machine start-up

    ``` ShellCommand
    $ ./bin/start-splice.sh
    ```

 


