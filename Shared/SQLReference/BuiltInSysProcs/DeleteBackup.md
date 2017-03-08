[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/DeleteBackup.html)

<a href="" id="BuiltInSysProcs.BackupDatabase"></a>[]()SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP
========================================================================================

The SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP system procedure deletes a backup that you previously created using either the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE](BackupDatabase.html)</span> or <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP](ScheduleDailyBackup.html)</span> system procedures.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_DELETE_BACKUP( BIGINT backupId ); 
```

backupId

Specifies the ID of the backup job you want to delete.

You can find the ID of a specific backup by querying the <span class="CodeFont">[SYS.SYSBACKUP](../SystemTables/SysBackup.html)</span> system table. See the [<span class="ItalicFont">Backing Up and Restoring</span>](../../../OnPremise/Administrators/BackupAndRestore.html) topic in our <span class="ItalicFont">Administrator's Guide</span> for more information.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

Example

If necessary, you can first query the <span class="CodeFont">[SYS.SYSBACKUP](../SystemTables/SysBackup.html)</span> system table to find the <span class="CodeFont">BACKUP\_ID</span> of the job you want to delete; entries in that table include timestamp information.

And then delete that job:

``` Example
splice> SELECT * FROM SYS.SYSBACKUP;
BACKUP_ID  |BEGIN_TIMESTAMP           |END_TIMESTAMP            |STATUS  |FILESYSTEM                                     |SCOPE |INCR&|INCREMENTAL_PARENT_&|BACKUP_ITEM
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
40975      |2015-11-25 09:32:53.04    |2015-11-25 09:33:09.081  |S       |/Users/me/Documents/splicemachine/dbBackups    |D     |false|-1                  |93         

1 row selected

splice> CALL SYSCS_UTIL.SYSCS_DELETE_BACKUP(40975); 
Statement executed.
```

See Also

-   [<span class="ItalicFont">Backing Up and Restoring Databases</span>](../../../OnPremise/Administrators/BackupAndRestore.html) in the <span class="ItalicFont">Administrator's Guide</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE</span>](BackupDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP</span>](CancelDailyBackup.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS</span>](DeleteOldBackups.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE</span>](RestoreDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP</span>](ScheduleDailyBackup.html) built-in system procedure
-   <span class="CodeFont">[SYSBACKUP](../SystemTables/SysBackup.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPITEMS](../SystemTables/SysBackupItems.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPJOBS](../SystemTables/SysBackupJobs.html)</span> system table

 


