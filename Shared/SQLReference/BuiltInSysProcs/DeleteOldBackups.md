[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/DeleteOldBackups.html)

[]()SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS
===========================================

The SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS system procedure deletes any backups that are older than a specified number of days (the <span class="ItalicFont">backup window</span>), retaining only those backups that fit into that window.

Backups can consume a lot of disk space, and thus, we recommend regularly scheduling both the creation of new backups and deletion of outdated backups.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_DELETE_OLD_BACKUPS( INT backupWindow ); 
```

backupWindow

Specifies the number of days of backups that you want retained. Any backups created more than <span class="CodeFont">backupWindow</span> days ago are deleted.

See the [<span class="ItalicFont">Backing Up and Restoring</span>](../../../OnPremise/Administrators/BackupAndRestore.html) topic in our <span class="ItalicFont">Administrator's Guide</span> for more information.

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

SQL Example

The following example deletes all database backups that were created more than 30 days ago.

``` Example
splice> CALL SYSCS_UTIL.SYSCS_DELETE_OLD_BACKUPS(30);
Statement executed.
```

See Also

-   [<span class="ItalicFont">Backing Up and Restoring Databases</span>](../../../OnPremise/Administrators/BackupAndRestore.html) in the <span class="ItalicFont">Administrator's Guide</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE</span>](BackupDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP</span>](CancelDailyBackup.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP</span>](DeleteBackup.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE</span>](RestoreDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP</span>](ScheduleDailyBackup.html) built-in system procedure
-   <span class="CodeFont">[SYSBACKUP](../SystemTables/SysBackup.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPITEMS](../SystemTables/SysBackupItems.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPJOBS](../SystemTables/SysBackupJobs.html)</span> system table

 


