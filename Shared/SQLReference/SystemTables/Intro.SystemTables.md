[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/Intro.SystemTables.html)

[]()System Tables
=================

This section contains the reference documentation for the Splice Machine SQL Statements, in the following subsections:

-   [Database Backups Tables](Intro.Backups.html)
-   [Database Objects Information Tables](Intro.DatabaseObjects.html)
-   [Database Permissions Tables](Intro.Permissions.html)
-   [Database Statistics Tables](Intro.Statistics.html)
-   [System Information Tables](Intro.SystemInfo.html)

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Since the system tables belong to the <span class="CodeFont">SYS</span> schema, you must preface any inquiries involving these tables with the <span class="CodeFont">SYS.</span> prefix.
You can use the Java <span class="CodeFont">java.sql.DatabaseMetaData</span> class to learn more about these tables.

Database Backups Tables

These are the System Tables with backups information:

| System Table                          | Description                                                                                                                                                          |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SYSBACKUP](SysBackup.html)           | Information about each run of a backup job that has been run for the database. You can query this table to determine status information about a specific backup job. |
| [SYSBACKUPITEMS](SysBackupItems.html) | Information about the items backed up for each backup job.                                                                                                           |
| [SYSBACKUPJOBS](SysBackupJobs.html)   | Information about all backup jobs that have been created for the database.                                                                                           |

Database Objects Tables

These are the System Tables with information about database objects:

| System Table                          | Description                                                                                            |
|---------------------------------------|--------------------------------------------------------------------------------------------------------|
| [SYSALIASES](SysAliases.html)         | Describes the procedures, functions, and user-defined types in the database.                           |
| [SYSCHECKS](SysChecks.html)           | Describes the check constraints within the current database.                                           |
| [SYSCOLUMNS](SysColumns.html)         | Describes the columns within all tables in the current database.                                       |
| [SYSCONSTRAINTS](SysConstraints.html) | Describes the information common to all types of constraints within the current database.              |
| [SYSDEPENDS](SysDepends.html)         | Stores the dependency relationships between persistent objects in the database.                        |
| [SYSFOREIGNKEYS](SysForeignKeys.html) | Describes the information specific to foreign key constraints in the current database.                 |
| [SYSKEYS](SysKeys.html)               | Describes the specific information for primary key and unique constraints within the current database. |
| [SYSROLES](SysRoles.html)             | Stores the roles in the database.                                                                      |
| [SYSSCHEMAS](SysSchemas.html)         | Describes the schemas within the current database.                                                     |
| [SYSSEQUENCES](SysSequences.html)     | Describes the sequence generators in the database.                                                     |
| [SYSTABLES](SysTables.html)           | Describes the tables and views within the current database.                                            |
| [SYSTRIGGERS](SysTriggers.html)       | Describes the triggers defined for the database.                                                       |
| [SYSVIEWS](SysViews.html)             | Describes the view definitions within the current database.                                            |

Database Permissions Tables

These are the System Tables with database permissions information:

| System Table                            | Description                                                                     |
|-----------------------------------------|---------------------------------------------------------------------------------|
| [SYSCOLPERMS](SysColPerms.html)         | Stores the column permissions that have been granted but not revoked.           |
| [SYSPERMS](SysPerms.html)               | Describes the usage permissions for sequence generators and user-defined types. |
| [SYSROUTINEPERMS](SysRoutinePerms.html) | Stores the permissions that have been granted to routines.                      |
| [SYSTABLEPERMS](SysTablePerms.html)     | Stores the table permissions that have been granted but not revoked.            |

Database Statistics Tables

These are the System Tables with database statistics information:

| System Table                                    | Description                                                          |
|-------------------------------------------------|----------------------------------------------------------------------|
| [SYSCOLUMNSTATISTICS](SysColumnStatistics.html) | Statistics gathered for each column in each table.                   |
| [SYSTABLESTATISTICS](SysTableStatistics.html)   | Describes the statistics for each table within the current database. |

System Information Tables

These are the System Tables with system information:

| System Table                              | Description                                                                                                                     |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| [SYSCONGLOMERATES](SysConglomerates.html) | Describes the conglomerates within the current database. A conglomerate is a unit of storage and is either a table or an index. |
| [SYSFILES](SysFiles.html)                 | Describes jar files stored in the database.                                                                                     |
| [SYSSTATEMENTS](SysStatements.html)       | Describes the prepared statements in the database.                                                                              |
| [SYSUSERS](SysUsers.html)                 | Stores user credentials when NATIVE authentication is enabled.                                                                  |

 


