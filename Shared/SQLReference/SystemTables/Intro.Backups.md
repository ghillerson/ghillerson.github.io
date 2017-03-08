[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/Intro.Backups.html)

[]()Backup Tables
=================

This section contains the reference documentation for the Splice Machine SQL System Tables containing information about backups.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Since the system tables belong to the <span class="CodeFont">SYS</span> schema, you must preface any inquiries involving these tables with the <span class="CodeFont">SYS.</span> prefix.

The Backup System Tables are:

| System Table                          | Description                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SYSBACKUP](SysBackup.html)           | Information about each run of a backup job that has been run for the database. You can query this table to determine status information about a specific backup job. |
| [SYSBACKUPITEMS](SysBackupItems.html) | Information about the items backed up for each backup job.                                                                                                           |
| [SYSBACKUPJOBS](SysBackupJobs.html)   | Information about all backup jobs that have been created for the database.                                                                                           |

 


