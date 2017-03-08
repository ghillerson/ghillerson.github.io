[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/ScheduleDailyBackup.html)

SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP
==========================================

You can use the <span class="CodeFont">SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP</span> to schedule a full or incremental backup job that runs at a specified time each day.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You specify the scheduled start hour of the backup in Greenwich Mean Time (GMT).

Note that you can subsequently cancel a scheduled backup job with the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP](CancelDailyBackup.html)</span> system procedure, which permanently unschedules the backup. For more information, see the <span class="ItalicFont">[Backing Up and Restoring](../../../OnPremise/Administrators/BackupAndRestore.html)</span> topic in our <span class="ItalicFont">Administrator's Guide</span>.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_SCHEDULE_DAILY_DATABASE( 
               VARCHAR backupDir,
               VARCHAR(30) backupType,
               INT startHour
);
```

backupDir

Specifies the path to the directory in which you want the backup stored. This can be a local directory if you're using the standalone version of Splice Machine, or a directory in your cluster's file system (HDFS or MapR-FS).

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You must have permissions set properly to use cloud storage as a backup destination. See [Backing Up to Cloud Storage](../../../OnPremise/Administrators/BackupAndRestore.html#Backing) in the <span class="ItalicFont">Administrator's Guide</span> for information about setting backup permissions properties.

Relative paths are resolved based on the current user directory. To avoid confusion, we strongly recommend that you use an absolute path when specifying the backup destination.

backupType

Specifies the type of backup that you want performed. This must be one of the following values: <span class="CodeFont">'full'</span> or "<span class="CodeFont">'incremental'</span>; any other value produces an error and the backup is not run.

Note that if you specify <span class="CodeFont">'incremental'</span>, Splice Machine checks the [<span class="CodeFont">SYS.SYSBACKUP</span>](../SystemTables/SysBackup.html) table to determine if there already is a backup for the system; if not, Splice Machine will perform a full backup, and subsequent backups will be incremental.

startHour

Specifies the hour (<span class="CodeFont">0-23</span>) <span class="BoldFont">in GMT</span> at which you want the backup to run each day. A value less than <span class="CodeFont">0</span> or greater than <span class="CodeFont">23</span> produces an error and the backup is not scheduled.

SQL Examples

The following example schedules a daily incremental backup that runs at 3 am (GMT) and gets stored in the hdfs:///home/backup/ directory:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_SCHEDULE_DAILY_BACKUP('hdfs:///home/backup', 'incremental', 3);
Statement executed;
```

The following example schedules the same backup and stores it on AWS:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_SCHEDULE_DAILY_BACKUP('s3://backup1234', 'incremental', 3);
Statement executed.
```

And this example schedules a daily backup at 6pm (GMT) on a standalone version of Splice Machine:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_SCHEDULE_DAILY_BACKUP('./dbBackups', 'full',18);
Statement executed.
```

See Also

-   [<span class="ItalicFont">Backing Up and Restoring Databases</span>](../../../OnPremise/Administrators/BackupAndRestore.html) in the <span class="ItalicFont">Administrator's Guide</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE</span>](BackupDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP</span>](CancelDailyBackup.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP</span>](DeleteBackup.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS</span>](DeleteBackup.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE</span>](RestoreDatabase.html) built-in system procedure
-   <span class="CodeFont">[SYSBACKUP](../SystemTables/SysBackup.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPITEMS](../SystemTables/SysBackupItems.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPJOBS](../SystemTables/SysBackupJobs.html)</span> system table

 


