[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/CancelDailyBackup.html)

[]()SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP
============================================

The SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP system procedure cancels a scheduled backup job.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Once you cancel a daily backup, it will no longer be scheduled to run.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_CANCEL_DAILY_BACKUP( BIGINT jobId );
```

jobId

A <span class="CodeFont">BIGINT</span> value that specifies which scheduled backup job you want to cancel.

You can find the <span class="ItalicFont">jobId</span> you want to cancel by querying the [<span class="CodeFont">SYS.SYSBACKUPJOBS</span>](../SystemTables/SysBackupJobs.html) system table. See the [<span class="ItalicFont">Backing Up and Restoring</span>](../../../OnPremise/Administrators/BackupAndRestore.html) topic in our <span class="ItalicFont">Administrator's Guide</span> for more information.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

Example

If necessary, you can first query the <span class="CodeFont">[SYSBACKUPJOBS](../SystemTables/SysBackupJobs.html)</span> system table to find the <span class="CodeFont">jobId</span> of the job you want to cancel.

And then cancel that job; for example:

``` Example
splice> SELECT * FROM SYS.SYSBACKUPJOBS;
JOB_ID      |FILESYSTEM                               |TYPE          |HOUR_OF_DAY|BEGIN_TIMESTAMP 
-------------------------------------------------------------------------------------------------
41069       |/~/Documents/splicemachine/dbBackups/    |full          |18         |09:41:05.455

1 row selected

splice> CALL SYSCS_UTIL.SYSCS_CANCEL_DAILY_BACKUP(41069); 
Statement executed.
```

See Also

-   [<span class="ItalicFont">Backing Up and Restoring Databases</span>](../../../OnPremise/Administrators/BackupAndRestore.html) in the <span class="ItalicFont">Administrator's Guide</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE</span>](BackupDatabase.html)built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP</span>](DeleteBackup.html)built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS</span>](DeleteOldBackups.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE</span>](RestoreDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP</span>](ScheduleDailyBackup.html) built-in system procedure
-   <span class="CodeFont">[SYSBACKUP](../SystemTables/SysBackup.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPITEMS](../SystemTables/SysBackupItems.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPJOBS](../SystemTables/SysBackupJobs.html)</span> system table

 


