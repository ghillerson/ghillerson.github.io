[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/RestoreDatabase.html)

<a href="" id="BuiltInSysProcs.BackupDatabase"></a>[]()SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE
===========================================================================================

The SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE system procedure restores your database to the state it was in when a specific backup was performed, using a backup that you previously created using either the <span class="CodeFont">[SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE](BackupDatabase.html)</span> system procedure or the <span class="CodeFont">[SYSCS\_UTIL\_SYSCS\_SCHEDULE\_DAILY\_BACKUP](ScheduleDailyBackup.html)</span> system procedure.

You can restore your database from any previous full or incremental backup.

There are several important things to know about restoring your database from a previous backup:

-   Restoring a database <span class="BoldFont">wipes out your database</span> and replaces it with what had been previously backed up.
-   You <span class="BoldFont">cannot use your cluster</span> while restoring your database.
-   You <span class="BoldFont">must reboot your database</span> after the restore is complete. See the [Shutting Down Your Database](../../../OnPremise/Administrators/ShuttingDownDatabase.html) and [Starting Your Database](../../../OnPremise/Administrators/StartingDatabase.html) topics in this book for instructions on restarting your database.

If you are restoring from an incremental backup, you must first restore from the most recent full backup, and then incrementally restore from each subsequent incremental backup. See [Example 2 below.](#Example)

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_RESTORE_DATABASE( VARCHAR backupDir,
                                   BIGINT backupId ); 
```

backupDir

Specifies the path to the directory containing the backup from which you want to restore your database. This can be a local directory if you're using the standalone version of Splice Machine, or a directory in your cluster's file system (HDFS or MapR-FS).

Relative paths are resolved based on the current user directory. To avoid confusion, we strongly recommend that you use an absolute path when specifying the backup location.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You must specify the backup's directory when you call this procedure because, if your database has become corrupted and needs to be restored, the data in the <span class="CodeFont">BACKUP.BACKUP</span> table (which includes the location of each backup) may also be corrupted.

backupId

The ID of the backup job from which you want to restore your database.

The system [Backups table](../SystemTables/SysBackup.html) stores information about your backup jobs, including the <span class="CodeFont">backupId</span> assigned to each. See the [<span class="ItalicFont">Backing Up and Restoring</span>](../../../OnPremise/Administrators/BackupAndRestore.html) topic in our <span class="ItalicFont">Administrator's Guide</span> for more information.

Usage

Restoring you database can take a while, and has several major implications:

> There are several important things to know about restoring your database from a previous backup:
>
> -   Restoring a database <span class="BoldFont">wipes out your database</span> and replaces it with what had been previously backed up.
> -   You <span class="BoldFont">cannot use your cluster</span> while restoring your database.
> -   You <span class="BoldFont">must reboot your database</span> after the restore is complete by first [Shutting Down Your Database](../../../OnPremise/Administrators/ShuttingDownDatabase.html) and then [Starting Your Database](../../../OnPremise/Administrators/StartingDatabase.html).

As noted at the top of this topic: if you are restoring from an incremental backup, you must first restore from the most recent full backup, and then incrementally restore from each subsequent incremental backup. See [Example 2 below.](#Example)

Results

This procedure does not return a result.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

Examples

The following example first queries the system backup table to find the ID of the backup from which we want to restore, and then initiates the restoration.

Stop using your database before backing up, and keep in mind that restoring a database may take several minutes, depending on the size of your database.

``` Example
splice> SELECT * FROM SYS.SYSBACKUP;
BACKUP_ID |BEGIN_TIMESTAMP          |END_TIMESTAMP            |STATUS    |FILESYSTEM      |SCOPE |INCR&|INCREMENTAL_PARENT_&|BACKUP_ITEM
----------------------------------------------------------------------------------------------------------------------------------------
74101     |2015-11-30 17:46:41.431  |2015-11-30 17:46:56.664  |S         |./dbBackups/    |D     |true |40975               |30         
40975     |2015-11-25 09:32:53.04   |2015-11-25 09:33:09.081  |S         |~/splicemachine |D     |false|-1                  |93         

2 rows selected

splice> CALL SYSCS_UTIL.SYSCS_RESTORE_DATABASE('./dbBackups/', 74101);
Statement executed.
```

Once the restoration is complete, reboot your database by the [Shutting Down Your Database](../../../OnPremise/Administrators/ShuttingDownDatabase.html) and then [Starting Your Database.](../../../OnPremise/Administrators/StartingDatabase.html)

### []()Example 2 : Restore the Database from a Series of Incremental Backups

In this example, you have been running a daily incremental backup and want to restore it to the most recent version. Let's call the backups B1, B2, B3, and B4:

-   Full backup <span class="CodeFont">B1,(ID=1274)</span>
-   First incremental backup <span class="CodeFont">B2 (ID=1275)</span>
-   Second incremental backup <span class="CodeFont">B3 (ID=1276)</span>
-   Third incremental backup <span class="CodeFont">B4 (ID=1277)</span>

To restore your database to the state it was in when the <span class="CodeFont">B4</span> backup was run; you'll need to follow these steps:

1.  Restore your database from the full backup, <span class="CodeFont">B1</span>.

    ``` AppCommand
    call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1274);
    ```

2.  Restart your database.
3.  Restore your database from incremental backup <span class="CodeFont">B2</span>:

    ``` AppCommand
    call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1275);
    ```

4.  Restart your database.
5.  Restore your database from incremental backup <span class="CodeFont">B3</span>:

    ``` AppCommand
    call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1276);
    ```

6.  Restart your database.
7.  Restore your database from incremental backup <span class="CodeFont">B4</span>:

    ``` AppCommand
    call SYSCS_UTIL.SYSCS_RESTORE_DATABASE('/home/backup', 1277);
    ```

8.  Restart your database.

See Also

-   [<span class="ItalicFont">Backing Up and Restoring Databases</span>](../../../OnPremise/Administrators/BackupAndRestore.html) in the <span class="ItalicFont">Administrator's Guide</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE</span>](BackupDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP</span>](CancelDailyBackup.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP</span>](DeleteBackup.html)built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS</span>](DeleteOldBackups.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP</span>](ScheduleDailyBackup.html) built-in system procedure
-   <span class="CodeFont">[SYSBACKUP](../SystemTables/SysBackup.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPITEMS](../SystemTables/SysBackupItems.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPJOBS](../SystemTables/SysBackupJobs.html)</span> system table

 


