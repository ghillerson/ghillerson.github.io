[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/CancelBackup.html)

[]()SYSCS\_UTIL.SYSCS\_CANCEL\_BACKUP
=====================================

The SYSCS\_UTIL.SYSCS\_CANCEL\_BACKUP system procedure cancels an in-progress backup.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_CANCEL_BACKUP( ); 
```

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

Example

This cancels the currently running backup:

``` Example
CALL SYSCS_UTIL.SYSCS_CANCEL_BACKUP(); 
```

See Also

-   [<span class="ItalicFont">Backing Up and Restoring Databases</span>](../../../OnPremise/Administrators/BackupAndRestore.html) in the <span class="ItalicFont">Administrator's Guide</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE</span>](BackupDatabase.html)built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP</span>](DeleteBackup.html)built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS</span>](DeleteOldBackups.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE</span>](RestoreDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP</span>](ScheduleDailyBackup.html) built-in system procedure

 


