[Open topic with navigation](../../index.html#OnPremise/Administrators/BackupAndRestore.html)

[]()Backing Up and Restoring Your Database
==========================================

<span class="noteEnterpriseNote">ENTERPRISE ONLY: This feature is available only with a Splice Machine Enterprise license.</span>

You cannot use this feature with the Community version of Splice Machine. For a list of the additional features available in the Enterprise edition, see our [Splice Machine Editions](../GettingStarted/SpliceEditions.html) page.

To obtain a license for the Splice Machine <span class="ItalicFont">Enterprise Edition</span>, <span class="noteEnterpriseNote">please [Contact Splice Machine Sales](http://www.splicemachine.com/company/contact-us/) today.</span>

Splice Machine provides built-in system procedures that make it easy to back up and restore your entire database. You can:

-   create full and incremental backups to run immediately
-   schedule daily full or incremental backups
-   restore your database from a backup
-   manage your backups
-   access logs of your backups

The rest of this topic will help you with working with your backups, in these sections:

-   [About Splice Machine Backups](#About)
-   [Using the Backup Operations](#Using)
-   [Backing Up to Cloud Storage](#Backing)

[]()About Splice Machine Backups
--------------------------------

Splice Machine supports: both full and incremental backups: 

-   A <span class="ItalicFont">full backup</span> backs up all of the files/blocks that constitute your database.
-   An <span class="ItalicFont">incremental backup</span> only stores database files/blocks that have changed since a previous backup.

Because backups can consume a lot of disk space, most customers define a backup strategy that blends their needs for security, recover-ability, and space restrictions. Since incremental backups require a lot less space than do full backups, and allow for faster recovery of data, many customers schedule daily, incremental backups.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Splice Machine automatically detects when it is the first run of an incremental backup and performs a one-time full backup; subsequent runs will only back up changed files/blocks.

### Backup IDs, Backup Jobs, and Backup Tables

Splice Machine uses <span class="ItalicFont">backup IDs</span> to identify a specific full or incremental <span class="ItalicFont">backup</span> that is stored on a file system, and <span class="ItalicFont">backup job IDs</span> to identify each scheduled <span class="ItalicFont">backup job</span>. Information about backups and backup jobs is stored in these system tables:

| System Table                                     | Contains Information About                                                                                                   |
|--------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| <span class="CodeFont">SYS.SYSBACKUP</span>      | Each database backup; you can query this table to find the ID of and details about a backup that was run at a specific time. |
| <span class="CodeFont">SYS.SYSBACKUPITEMS</span> | Each item (table) in a backup.                                                                                               |
| <span class="CodeFont">SYS.SYSBACKUPJOBS</span>  | Each backup job that has been run for the database.                                                                          |

### Temporary Tables and Backups

There's a subtle issue with performing a backup when you're using a temporary table in your session: although the temporary table is (correctly) not backed up, the temporary table's entry in the system tables will be backed up. When the backup is restored, the table entries will be restored, but the temporary table will be missing.

There's a simple workaround:

1.  Exit your current session, which will automatically delete the temporary table and its system table entries.
2.  Start a new session (reconnect to your database).
3.  Start your backup job.

[]()Using the Backup Operations
-------------------------------

This section summarizes and provides examples of using the Splice Machine backup operations:

-   [Scheduling a Daily Backup Job](#Scheduling)
-   [Running an Immediate Backup](#Running)
-   [Restoring Your Database From a Previous Backup](#Restorin)
-   [Reviewing Backup Information](#Reviewing)
-   [Canceling a Scheduled Backup Job](#Cancelin)
-   <a href="#CancelB" class="WithinBook">Canceling a Backup That's In Progress</a>
-   [Deleting a Backup](#Deleting)
-   [Deleting Outdated Backups](#DeleteOld)

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You must make sure that the directory to which you are backing up or from which data is being restored is accessible to the HBase user who is initiating the restore. Make sure the directory permissions are set correctly on the backup directory.
Note that you can store your backups in a cloud-based storage service such as AWS; for more information, see the [Backing Up to Cloud Storage](#Backing) section below.

### []()Scheduling a Daily Backup Job

Use the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP](../../Shared/SQLReference/BuiltInSysProcs/ScheduleDailyBackup.html)</span> system procedure to schedule a job that performs a daily incremental or full backup of your database:

``` FcnSyntax
SYSCS_UTIL.SYSCS_SCHEDULE_DAILY_BACKUP( backupDir, backupType, startHour );
```

backupDir

A <span class="CodeFont">VARCHAR</span> value that specifies the path to the directory in which you want the backup stored.

Note that this directory can be cloud-based, as described in the [Backing Up to Cloud Services](#Backing) section below.

backupType

A <span class="CodeFont">VARCHAR(30)</span> value that specifies the type of backup that you want performed; one of the following values: <span class="CodeFont">full</span> or <span class="CodeFont">incremental</span>. The first run of an incremental backup is always a full backup.

startHour

Specifies the hour (<span class="CodeFont">0-23</span>) in GMT at which you want the backup to run each day. A value less than <span class="CodeFont">0</span> or greater than <span class="CodeFont">23</span> produces an error and the backup is not scheduled.

#### Example 1: Set up a full backup to run every day at 3am:

To run a full backup every night at 3am:

``` AppCommand
call SYSCS_UTIL.SYSCS_SCHEDULE_DAILY_BACKUP('/home/backup', 'full', 3);
```

#### Example 2: Set up an incremental backup to run every day at noon:

To run an incremental backup every day at noon.

``` AppCommand
call SYSCS_UTIL.SYSCS_BACKUP_DATABASE('/home/backup', 'incremental', 12);
```

### []()Running an Immediate Backup

Use the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE](../../Shared/SQLReference/BuiltInSysProcs/BackupDatabase.html)</span> system procedure to immediately run a full or incremental backup.

``` FcnSyntax
SYSCS_UTIL.SYSCS_BACKUP_DATABASE( backupDir, backupType );
```

backupDir

A <span class="CodeFont">VARCHAR</span> value that specifies the path to the directory in which you want the backup stored.

Note that this directory can be cloud-based, as described in the [Backing Up to Cloud Services](#Backing) section below.

backupType

A <span class="CodeFont">VARCHAR(30)</span> value that specifies the type of backup that you want performed; use.one of the following values: <span class="CodeFont">full</span> or <span class="CodeFont">incremental</span>.

#### Example 1: Execute a full backup now

To execute a backup right now:

``` AppCommand
call SYSCS_UTIL.SYSCS_BACKUP_DATABASE('/home/backup', 'full');
```

#### Example 2: Execute an incremental backup now:

This call will run an incremental backup right now. Splice Machine checks the <span class="CodeFont">[SYSBACKUP System Table](../../Shared/SQLReference/SystemTables/SysBackup.html)</span> to determine if there already is a backup for the system; if not, Splice Machine will perform a full backup, and subsequent backups will be incremental. The backup data is stored in the specified directory.

``` AppCommand
call SYSCS_UTIL.SYSCS_BACKUP_DATABASE('/home/backup', 'incremental');
```

### []()Restoring Your Database From a Previous Backup

You can restore your database from a previous backup, use the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE](../../Shared/SQLReference/BuiltInSysProcs/RestoreDatabase.html)</span> system procedure. Note that if you've been using incremental backups, you will need to first restore from the initial full backup, and then successively restore from each incremental backup. See the examples section below.

To restore your database from a previous backup, use the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE](../../Shared/SQLReference/BuiltInSysProcs/RestoreDatabase.html)</span> system procedure:

``` FcnSyntax
SYSCS_UTIL.SYSCS_RESTORE_DATABASE(backupDir, backupId); 
```

backupDir

A <span class="CodeFont">VARCHAR</span> value that specifies the path to the directory in which the backup isstored.

You can find the <span class="ItalicFont">backupId</span> you want to use by querying the <span class="CodeFont">[SYSBACKUP System Table](../../Shared/SQLReference/SystemTables/SysBackup.html)</span>. See the [Reviewing Backup Information](#Reviewing) section below for more information.

backupId

A <span class="CodeFont">BIGINT</span> value that specifies which backup you want to use to restore your database.

> There are several important things to know about restoring your database from a previous backup:
>
> -   Restoring a database <span class="BoldFont">wipes out your database</span> and replaces it with what had been previously backed up.
> -   You <span class="BoldFont">cannot use your cluster</span> while restoring your database.
> -   You <span class="BoldFont">must reboot your database</span> after the restore is complete by first [Shutting Down Your Database](ShuttingDownDatabase.html) and then [Starting Your Database](StartingDatabase.html).

> #### Example 1: Restore the database from a local, full backup
>
> This example restores your database from the backup stored in the <span class="CodeFont">/home/backup</span> directory that has <span class="CodeFont">backupId=1273</span>:
>
> ``` AppCommand
> call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1273);
> ```
>
> #### Example 2: Restore the database from a series of incremental backups
>
> In this example, you have been running a daily incremental backup and want to restore it to the most recent version. Let's call the backups B1, B2, B3, and B4:
>
> -   Full backup <span class="CodeFont">B1,(ID=1274)</span>
> -   First incremental backup <span class="CodeFont">B2 (ID=1275)</span>
> -   Second incremental backup <span class="CodeFont">B3 (ID=1276)</span>
> -   Third incremental backup <span class="CodeFont">B4 (ID=1277)</span>
>
> To restore your database to the state it was in when the <span class="CodeFont">B4</span> backup was run; you'll need to follow these steps:
>
> 1.  Restore your database from the full backup, <span class="CodeFont">B1</span>.
>
>     ``` AppCommand
>     call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1274);
>     ```
>
> 2.  Restart your database.
> 3.  Restore your database from incremental backup <span class="CodeFont">B2</span>:
>
>     ``` AppCommand
>     call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1275);
>     ```
>
> 4.  Restart your database.
> 5.  Restore your database from incremental backup <span class="CodeFont">B3</span>:
>
>     ``` AppCommand
>     call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1276);
>     ```
>
> 6.  Restart your database.
> 7.  Restore your database from incremental backup <span class="CodeFont">B4</span>:
>
>     ``` AppCommand
>     call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1277);
>     ```
>
> 8.  Restart your database.
>
### []()Reviewing Backups

Splice Machine stores information about your backups and scheduled backup jobs in system tables that you can query, and stores a backup log file in the directory to which a backup is written when it runs.

#### Backup Job Information

Information about your scheduled backup jobs is stored in the <span class="CodeFont">[SYSBACKUPJOBS System Table](../../Shared/SQLReference/SystemTables/SysBackupJobs.html)</span>:

``` Example
splice> select * from SYS.SYSBACKUPJOBS;
JOB_ID         |FILESYSTEM        |TYPE           |HOUR_OF_DAY|BEGIN_TIMESTAMP
--------------------------------------------------------------------------------------
22275          |/data/backup/0101 |FULL           |22         |2015-04-03 18:43:42.631
```

You can query this table to find a job ID, if you need to cancel a scheduled backup.

#### Backup Information

Information about each backup of your database is stored in the <span class="CodeFont">[SYSBACKUP System Table](../../Shared/SQLReference/SystemTables/SysBackup.html)</span>, including the ID assigned to the backup and its location. You can query this table to find the ID of a specific backup, which you need if you want to restore your database from it, or to delete it:

``` Example
splice> select * from SYS.SYSBACKUP;
BACKUP_ID |BEGIN_TIMESTAMP         |END_TIMESTAMP           |STATUS |FILESYSTEM        |SCOPE |INCR&|INCREMENTAL_PARENT_&|BACKUP_ITEM
------------------------------------------------------------------------------------------------------------------------------------------
22275     |2015-04-03 18:40:56.877 |2015-04-03 18:43:42.631 |S      |/data/backup/0101 |D     |false|-1       |15
21428     |2015-04-03 18:30:55.964 |2015-04-03 18:33:49.494 |S      |/data/backup/0101 |D     |false|-1       |15
20793     |2015-04-03 18:23:53.574 |2015-04-03 18:27:07.07  |S      |/data/backup/0101 |D     |false|-1       |87
```

#### Backup Log Files

When you run a backup, a log file is created or updated in the directory in which the backup is stored. This log file is named <span class="CodeFont">backupStatus.log</span>, and is stored in plain text, human-readable format. Here's a sample snippet from a log file:

``` Example
Expected time for backup ~12 hours, expected finish at 15:30 on April 8, 2015
5 objects of 833 objects backed up..
6 objects of 833 objects backed up…
…
Finished with Success. Total time taken for backup was 11 hours 32 minutes.
```

### []()Canceling a Scheduled Backup

You can cancel a daily backup with the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP](../../Shared/SQLReference/BuiltInSysProcs/CancelDailyBackup.html)</span> system procedure:

``` FcnSyntax
SYSCS_UTIL.SYSCS_CANCEL_DAILY_BACKUP( jobId ); 
```

jobId

A <span class="CodeFont">BIGINT</span> value that specifies which scheduled backup job you want to cancel.

You can find the <span class="ItalicFont">jobId</span> you want to cancel by querying the <span class="CodeFont">[SYSBACKUPJOBS System Table](../../Shared/SQLReference/SystemTables/SysBackupJobs.html)</span>. See the [Reviewing Backup Information](#Reviewing) section below for information about using the the <span class="CodeFont">[SYSBACKUPJOBS System Table](../../Shared/SQLReference/SystemTables/SysBackupJobs.html)</span>.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Once you cancel a daily backup, it will no longer be scheduled to run.

#### Example: Cancel a daily backup

This example cancels the backup that has <span class="CodeFont">jobId=1273</span>:

``` AppCommand
call SYSCS_UTIL.SYSCS_CANCEL_DAILY_BACKUP(1273);
```

### []()Canceling a Backup That's In Progress

You can call the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_CANCEL\_BACKUP](../../Shared/SQLReference/BuiltInSysProcs/CancelBackup.html)</span> system procedure to cancel a backup that is currently running:

``` FcnSyntax
SYSCS_UTIL.SYSCS_CANCEL_BACKUP(  ); 
```

#### Example: Cancel a running backup

This example cancels the Splice Machine backup job that is currently running.

``` AppCommand
call SYSCS_UTIL.SYSCS_CANCEL_BACKUP();
```

### []()Deleting a Backup

Use the [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP</span>](../../Shared/SQLReference/BuiltInSysProcs/DeleteBackup.html) system procedure to delete a single backup:

``` FcnSyntax
SYSCS_UTIL.SYSCS_DELETE_BACKUP( backupId ); 
```

backupId

A <span class="CodeFont">BIGINT</span> value that specifies which backup you want to delete.

You can find the <span class="ItalicFont">backupId</span> you want to delete by querying the <span class="CodeFont">[SYSBACKUP System Table](../../Shared/SQLReference/SystemTables/SysBackup.html)</span>, See the [Reviewing Backup Information](#Reviewing) section below for information about using the <span class="CodeFont">[SYSBACKUP System Table](../../Shared/SQLReference/SystemTables/SysBackup.html)</span>,

#### Example: Delete a backup

This example deletes the backup that has <span class="CodeFont">backupId=1273</span>:

``` AppCommand
call SYSCS_UTIL.SYSCS_DELETE_BACKUP(1273);
```

### []()Deleting Outdated Backups

Use the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS](../../Shared/SQLReference/BuiltInSysProcs/DeleteOldBackups.html)</span> system procedure to delete all backups that are older than a certain number of days.

``` FcnSyntax
SYSCS_UTIL.SYSCS_DELETE_OLD_BACKUPS( backupWindow ); 
```

backupWindow

An <span class="CodeFont">INT</span> value that specifies the number of days of backups that you want retained. Any backups created more than <span class="CodeFont">backupWindow</span> days ago are deleted.

#### Example: Delete all backups more than a week old

This example deletes all backups that are more than a week old:

``` AppCommand
call SYSCS_UTIL.SYSCS_DELETE_OLD_BACKUPS(7);
```

[]()Backing Up to Cloud Storage - AWS
-------------------------------------

You can specify cloud-based directories as destinations for your backups. This section describes how to set up credentials to allow Splice Machine to create and manage backups on AWS.

You need to enable backups by storing your AWS Access Key ID and Secret Access Key values in your cluster's HDFS core-site.xml file: how you set up your credentials depends on the Hadoop platform you are using; see the section below for your platform:

<span class="BoldFont">IMPORTANT:</span> You must have access to the S3 bucket to which you are backing up your database. The instructions below give general guidelines; however, S3 access differs in every deployment. For more information, see these sites:

-   <http://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html>
-   [https://wiki.apache.org/hadoop/AmazonS3](http://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html)

-   [Enabling backups on CDH](#Enabling)
-   [Enabling backups on HDP](#Enabling2)
-   [Enabling backups on MapR](#Enabling3)

### []()Enabling Splice Machine Backups on CDH

You can use Cloudera Manager to configure properties to enable Splice Machine backups; follow these steps:

1.  Navigate to the Cloudera Manager home screen.
2.  Stop both HBase and HDFS: 

    -   Click the <span class="AppCommand">HBase Actions</span> drop-down arrow associated with (to the right of) <span class="CodeFont">HBase</span> in the cluster summary section of the home screen, and then click <span class="AppCommand">Stop</span> to stop HBase.
    -   Click the <span class="AppCommand">HDFS Actions</span> drop-down arrow associated with (to the right of) and then click <span class="AppCommand">Stop</span> to stop HDFS.

3.  Click <span class="AppCommand">HDFS</span> in the Cloudera Manager home screen, then click the <span class="AppCommand">Configuration</span> tab, and in category, click <span class="AppCommand">Advanced</span>. Then set these property values in the <span class="CodeFont">Cluster-wide Advanced Configuration Snippet (Safety Valve) for core-site.xml</span> field:
    ``` AppCommand
    fs.s3.awsAccessKeyId       = <Your AWS Access Key>
    fs.s3.awsSecretAccessKey   = <Your AWS Access Secret Key>
    ```

4.  Restart both services:

    -   Click the <span class="AppCommand">HDFS Actions</span> drop-down arrow associated with (to the right of) HDFS in the cluster summary section of the Cloudera Manager home screen, and then click <span class="AppCommand">Start</span> to restart HDFS.
    -   Navigate to the <span class="ItalicFont">HBase Status</span> tab in Cloudera Manager. Then, using the <span class="AppCommand">Actions</span> drop-down in the upper-right corner, click <span class="AppCommand">Start</span> to create a start HBase.

### []()Enabling Splice Machine Backups on HDP

You can use the Ambari dashboard to configure these properties. Follow these steps:

1.  Navigate to the HDFS <span class="AppCommand">Configs</span> screen.
2.  Select the <span class="AppCommand">Services</span> tab at the top of the Ambari dashboard screen, then stop both HBase and HDFS: 

    -   Click <span class="AppCommand">HBase</span> in the left pane of the screen, then click <span class="AppCommand">Service Actions-&gt;Stop</span> in the upper-right portion of the Ambari screen.
    -   Click <span class="AppCommand">HDFS</span> in the left pane of the screen, the click <span class="AppCommand">Service Actions-&gt;Stop</span>.

3.  Select <span class="AppCommand">Custom core-site</span> and add these properties:
    ``` AppCommand
    fs.s3.awsAccessKeyId       = <Your AWS Access Key>
    fs.s3.awsSecretAccessKey   = <Your AWS Secret Access Key>
    ```

4.  Restart both services:

    -   Click <span class="AppCommand">HDFS</span> in the left pane of the screen, the click <span class="AppCommand">Service Actions-&gt;Restart All</span>.
    -   Click <span class="AppCommand">HBase</span> in the left pane of the screen, the click <span class="AppCommand">Service Actions-&gt;Restart All</span>.

### []()Enabling Splice Machine Backups on MapR

To enable Amazon S3 access on a MapR cluster, you must stop services, change the configuration files on each node, and then restart services. Follow these steps:

1.  Stop all MapR services by stopping the warden service on each host:

    ``` ShellCommand
    sudo service mapr-warden stop
    ```

2.  You need to edit two files on each MapR-FS fileserver and HBase RegionServer in your cluster to allow hosts access to Amazon S3. You need to provide the fs.s3 access key ID and secret in each of these files:

    -   <span class="CodeFont">/opt/mapr/hadoop/hadoop-2.x.x/etc/hadoop/core-site.xml</span> for <span class="ItalicFont">Hadoop/MapReduce/YARN 2.x</span> site configuration
    -   <span class="CodeFont">/opt/mapr/hadoop/hadoop-0.x.x/conf/core-site.xml</span> for <span class="ItalicFont">Hadoop/MapReduce 0.x/1.x</span> site configuration

    If both <span class="ItalicFont">MapReduce v1</span> and <span class="ItalicFont">YARN/MapReduce 2</span> are installed on the MapR compute hosts, the newer <span class="ItalicFont">hadoop-2.x.x</span> version of the file will be canonical, and the older <span class="ItalicFont">hadoop-0.x.x</span> file symbolically linked to it. You can check this using the following <span class="CodeFont">ls</span> and <span class="CodeFont">file</span> commands:

    ``` ShellCommand
    $ ls -al /opt/mapr/hadoop/hadoop-0*/conf/core-site.xml /opt/mapr/hadoop/hadoop-2*/etc/hadoop/core-site.xml
    lrwxrwxrwx 1 mapr root  54 Apr 24 11:01 /opt/mapr/hadoop/hadoop-0.20.2/conf/core-site.xml -> /opt/mapr/hadoop/hadoop-2.5.1/etc/hadoop/core-site.xml
    -rw-r--r-- 1 mapr root 775 Apr 24 12:50 /opt/mapr/hadoop/hadoop-2.5.1/etc/hadoop/core-site.xml
    ```

    ``` ShellCommand
    $ file /opt/mapr/hadoop/hadoop-0*/conf/core-site.xml /opt/mapr/hadoop/hadoop-2*/etc/hadoop/core-site.xml
    /opt/mapr/hadoop/hadoop-0.20.2/conf/core-site.xml:      symbolic link to `/opt/mapr/hadoop/hadoop-2.5.1/etc/hadoop/core-site.xml'
    /opt/mapr/hadoop/hadoop-2.5.1/etc/hadoop/core-site.xml: XML  document text
    ```

3.  Add your access key ID and secret key in each file by adding the following properties between the <span class="CodeFont">&lt;configuration&gt;</span> and <span class="CodeFont">&lt;/configuration&gt;</span> tags:

    ``` AppCommand
    <!-- AWS s3://bucket/... block-based access -->
    <property>
    <name>fs.s3.awsAccessKeyId</name>
    <value>_AWS_ACCESS_KEY_ID_</value>
    </property>
    <property>
    <name>fs.s3.awsSecretAccessKey</name>
    <value>_AWS_SECRET_ACCESS_KEY_</value>
    </property>
    <!-- AWS s3n://bucket/... filesystem-like access -->
    <property>
    <name>fs.s3n.awsAccessKeyId</name>
    <value>_AWS_ACCESS_KEY_ID_</value>
    </property>
    <property>
    <name>fs.s3n.awsSecretAccessKey</name>
    <value>_AWS_SECRET_ACCESS_KEY_</value>
    </property>
    ```

4.  Use the <span class="CodeFont">hadoop</span> command to view your configuration changes:

    ``` ShellCommand
    $ hadoop conf | grep fs\\.s3 | grep -i access | sort -u
    <property><name>fs.s3.awsAccessKeyId</name><value>_AWS_ACCESS_KEY_ID_</value><source>core-site.xml</source></property>
    <property><name>fs.s3.awsSecretAccessKey</name><value>_AWS_SECRET_ACCESS_KEY_</value><source>core-site.xml</source></property>
    <property><name>fs.s3n.awsAccessKeyId</name><value>_AWS_ACCESS_KEY_ID_</value><source>core-site.xml</source></property>
    <property><name>fs.s3n.awsSecretAccessKey</name><value>_AWS_SECRET_ACCESS_KEY_</value><source>core-site.xml</source></property>
    ```

5.  You can also verify that access is correctly configured with the <span class="CodeFont">hadoop</span> command to list the contents of an existing bucket. For example:

    ``` ShellCommand
    sudo -iu mapr hadoop fs -ls s3n://yourbucketname/
    ```

6.  Finally, restart MapR services on each node via MapR's warden::

    ``` ShellCommand
    sudo service mapr-warden start
    ```

See Also
--------

-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE](../../Shared/SQLReference/BuiltInSysProcs/BackupDatabase.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_CANCEL\_BACKUP](../../Shared/SQLReference/BuiltInSysProcs/CancelBackup.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP](../../Shared/SQLReference/BuiltInSysProcs/CancelDailyBackup.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP](../../Shared/SQLReference/BuiltInSysProcs/DeleteBackup.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS](../../Shared/SQLReference/BuiltInSysProcs/DeleteOldBackups.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE](../../Shared/SQLReference/BuiltInSysProcs/RestoreDatabase.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP](../../Shared/SQLReference/BuiltInSysProcs/ScheduleDailyBackup.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSBACKUP System Table](../../Shared/SQLReference/SystemTables/SysBackup.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSBACKUPITEMS System Table](../../Shared/SQLReference/SystemTables/SysBackupItems.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>
-   <span class="CodeFont">[SYSBACKUPJOBS System Table](../../Shared/SQLReference/SystemTables/SysBackupJobs.html)</span> in the <span class="ItalicFont">SQL Reference Manual</span>

 


