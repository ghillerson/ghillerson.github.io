[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/BackupDatabase.html)

<a href="" id="BuiltInSysProcs.BackupDatabase"></a>[]()SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE
==========================================================================================

The SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE system procedure performs an immediate full or incremental backup of your database to a specified backup directory.

Splice Machine supports both full and incremental backups: 

-   A <span class="ItalicFont">full backup</span> backs up all of the files/blocks that constitute your database.
-   An <span class="ItalicFont">incremental backup</span> only stores database files/blocks that have changed since a previous backup.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>The first time that you run an incremental backup, a full backup is performed. Subsequent runs of the backup will only copy information that has changed since the previous backup.

For more information, see the [<span class="ItalicFont">Backing Up and Restoring</span>](../../../OnPremise/Administrators/BackupAndRestore.html) topic in our <span class="ItalicFont">Administrator's Guide</span>.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_BACKUP_DATABASE( VARCHAR backupDir,
                                  VARCHAR(30) backupType );
```

backupDir

Specifies the path to the directory in which you want the backup stored. This can be a local directory if you're using the standalone version of Splice Machine, or a directory in your cluster's file system (HDFS or MapR-FS).

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You must have permissions set properly to use cloud storage as a backup destination. See [Backing Up to Cloud Storage](../../../OnPremise/Administrators/BackupAndRestore.html#Backing) in the <span class="ItalicFont">Administrator's Guide</span> for information about setting backup permissions properties.

Relative paths are resolved based on the current user directory. To avoid confusion, we strongly recommend that you use an absolute path when specifying the backup destination.

backupType

Specifies the type of backup that you want performed.This must be one of the following values: <span class="CodeFont">'full'</span> or <span class="CodeFont">'incremental'</span>; any other value produces an error and the backup is not run.

Note that if you specify <span class="CodeFont">'incremental'</span>, Splice Machine checks the [<span class="CodeFont">SYS.SYSBACKUP</span>](../SystemTables/SysBackup.html) table to determine if there already is a backup for the system; if not, Splice Machine will perform a full backup, and subsequent backups will be incremental.

Results

This procedure does not return a result.

Usage Notes

There's a subtle issue with performing a backup when you're using a temporary table in your session: although the temporary table is (correctly) not backed up, the temporary table's entry in the system tables will be backed up. When the backup is restored, the table entries will be restored, but the temporary table will be missing.

There's a simple workaround:

1.  Exit your current session, which will automatically delete the temporary table and its system table entries.
2.  Start a new session (reconnect to your database).
3.  Start your backup job.

Execute Privileges

If authentication and SQL authorization are both enabled, only the database owner has execute privileges on this function by default. The database owner can grant access to other users.

JDBC example

The following example performs an immediate full backup to a subdirectory of the hdfs:///home/backup directory:

``` Example
CallableStatement cs = conn.prepareCall
  ("CALL SYSCS_UTIL.SYSCS_BACKUP_DATABASE(?,?)");
  cs.setString(1, 'hdfs:///home/backup');
  cs.setString(2, 'full'); 
  cs.execute();
  cs.close();
```

SQL Example

<span class="autonumber"><span class="noteAutoNum">RELEASE NOTE:  </span></span>Backing up a database may take several minutes, depending on the size of your database and how much of it you're backing up.

The following example runs an immediate incremental backup to the hdfs:///home/backup/ directory:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_BACKUP_DATABASE( 'hdfs:///home/backup', 'incremental' );
Statement executed.
```

The following example runs the same backup and stores it on AWS:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_BACKUP_DATABASE( 's3://backup1234', 'incremental' );
Statement executed.
```

And this example does a full backup to a relative directory (relative to your <span class="CodeFont">splicemachine</span> directory) on a standalone version of Splice Machine:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_BACKUP_DATABASE( './dbBackups', 'full' );
Statement executed.
```

See Also

-   [<span class="ItalicFont">Backing Up and Restoring Databases</span>](../../../OnPremise/Administrators/BackupAndRestore.html) in the <span class="ItalicFont">Administrator's Guide</span>
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP</span>](CancelDailyBackup.html)built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP</span>](DeleteBackup.html)built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS</span>](DeleteOldBackups.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE</span>](RestoreDatabase.html) built-in system procedure
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP</span>](ScheduleDailyBackup.html) built-in system procedure
-   <span class="CodeFont">[SYSBACKUP](../SystemTables/SysBackup.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPITEMS](../SystemTables/SysBackupItems.html)</span> system table
-   <span class="CodeFont">[SYSBACKUPJOBS](../SystemTables/SysBackupJobs.html)</span> system table

 


