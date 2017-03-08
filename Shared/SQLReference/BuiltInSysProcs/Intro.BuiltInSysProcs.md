[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/Intro.BuiltInSysProcs.html)

[]()Built-in System Procedures and Functions
============================================

This section contains the reference documentation for the Splice Machine Built-in SQL System Procedures and Functions, in the following subsections:

-   [Database Admin Procedures and Functions](#DatabaseAdmin)
-   [Database Property Procedures and Functions](#DatabaseProps)
-   [Importing Data Procedures and Functions](#Importing)
-   [Jar File Procedures and Functions](#Jar)
-   [Logging Procedures and Functions](#Logging)
-   [Statements and Stored Procedures System Procedures](#Statement)
-   [Statistics Procedures and Functions](#Statistics)
-   [System Status Procedures and Functions](#SystemStatus)
-   [Transaction Procedures and Functions](#Transaction)

[]()Database Admin Procedures and Functions

These are the system procedures and functions for administering your database:

| Procedure / Function Name                                                                        | Description                                                                                                                                                   |
|--------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_BACKUP\_DATABASE](BackupDatabase.html)                                       | Backs up the database to a specified backup directory.                                                                                                        |
| [SYSCS\_UTIL.SYSCS\_CANCEL\_BACKUP](CancelBackup.html)                                           | Cancels a backup.                                                                                                                                             |
| [SYSCS\_UTIL.SYSCS\_CANCEL\_DAILY\_BACKUP](CancelDailyBackup.html)                               | Cancels a scheduled daily backup.                                                                                                                             |
| [SYSCS\_UTIL.SYSCS\_CREATE\_USER](CreateUser.html)                                               | Adds a new user account to a database.                                                                                                                        |
| [SYSCS\_UTIL.SYSCS\_DELETE\_BACKUP](DeleteBackup.html)                                           | Delete a specific backup.                                                                                                                                     |
| [SYSCS\_UTIL.SYSCS\_DELETE\_OLD\_BACKUPS](DeleteOldBackups.html)                                 | Deletes all backups that were created more than a certain number of days ago.                                                                                 |
| [SYSCS\_UTIL.SYSCS\_DROP\_USER](DropUser.html)                                                   | Removes a user account from a database.                                                                                                                       |
| [SYSCS\_UTIL.SYSCS\_MODIFY\_PASSWORD](ModifyPassword.html)                                       | Called by a user to change that user's own password.                                                                                                          |
| [SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_SCHEMA](PerformMajorCompactionOnSchema.html) | Performs a major compaction on a schema                                                                                                                       |
| [SYSCS\_UTIL.SYSCS\_PERFORM\_MAJOR\_COMPACTION\_ON\_TABLE](PerformMajorCompactionOnTable.html)   | Performs a major compaction on a table.                                                                                                                       |
| [SYSCS\_UTIL.SYSCS\_REFRESH\_EXTERNAL\_TABLE](RefreshExternalTable.html)                         | Refreshes the schema of an external table in Splice Machine; use this when the schema of the table's source file has been modified outside of Splice Machine. |
| [SYSCS\_UTIL.SYSCS\_RESET\_PASSWORD](ResetPassword.html)                                         | Resets a password that has expired or has been forgotten.                                                                                                     |
| [SYSCS\_UTIL.SYSCS\_RESTORE\_DATABASE](RestoreDatabase.html)                                     | Restores a database from a previous backup.                                                                                                                   |
| [SYSCS\_UTIL.SYSCS\_SCHEDULE\_DAILY\_BACKUP](DeleteBackup.html)                                  | Schedules a full or incremental database backup to run at a specified time daily.                                                                             |
| [SYSCS\_UTIL.SYSCS\_UPDATE\_SCHEMA\_OWNER](UpdateSchemaOwner.html)                               | Changes the owner of a schema.                                                                                                                                |
| [SYSCS\_UTIL.VACUUM](Vacuum.html)                                                                | Performs clean-up operations on the system.                                                                                                                   |

[]()Database Properties Procedures and Functions

These are the system procedures and functions for working with your database properties:

| Procedure / Function Name                                                       | Description                                                                                                                                                                                               |
|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_GET\_ALL\_PROPERTIES](GetAllProperties.html)                | Displays all of the Splice Machine Derby properties.                                                                                                                                                      |
| [SYSCS\_UTIL.SYSCS\_GET\_DATABASE\_PROPERTY function](GetDatabaseProperty.html) | Fetches the value of the specified property of the database on the current connection.                                                                                                                    |
| [SYSCS\_UTIL.SYSCS\_GET\_SCHEMA\_INFO](GetSchemaInfo.html)                      | Displays table information for all user schemas, including the HBase regions occupied and their store file size.                                                                                          |
| [SYSCS\_UTIL.SYSCS\_PEEK\_AT\_SEQUENCE function](PeekAtSequence.html)           | Allows users to observe the instantaneous current value of a sequence generator without having to query the [<span class="CodeFont">SYSSEQUENCES</span> system table](../SystemTables/SysSequences.html). |
| [SYSCS\_UTIL.SYSCS\_SET\_DATABASE\_PROPERTY](SetDatabaseProperty.html)          | Sets or deletes the value of a property of the database on the current connection.                                                                                                                        |

[]()Importing Data Procedures and Functions

These are the system procedures and functions for importing data into your database:

| Procedure / Function Name                                              | Description                                                               |
|------------------------------------------------------------------------|---------------------------------------------------------------------------|
| [SYSCS\_UTIL.IMPORT\_DATA](ImportData.html)                            | Imports data to a subset of columns in a table.                           |
| [SYSCS\_UTIL.SYSCS\_UPSERT\_DATA\_FROM\_FILE](UpsertDataFromFile.html) | Checks upsert data without actually performing the insertions or updates. |

[]()Jar File Procedures and Functions

These are the system procedures and functions for working with JAR files:

| Procedure / Function Name                | Description                         |
|------------------------------------------|-------------------------------------|
| [SQLJ.INSTALL\_JAR](SQLJInstallJar.html) | Stores a jar file in a database.    |
| [SQLJ.REMOVE\_JAR](SQLJRemoveJar.html)   | Removes a jar file from a database. |
| [SQLJ.REPLACE\_JAR](SQLJReplaceJar.html) | Replaces a jar file in a database.  |

[]()Logging Procedures and Functions

These are the system procedures and functions for working with system logs:

| Procedure / Function Name                                    | Description                                                     |
|--------------------------------------------------------------|-----------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_GET\_LOGGER\_LEVEL](GetLoggerLevel.html) | Displays the log level of the specified logger.                 |
| [SYSCS\_UTIL.SYSCS\_GET\_LOGGERS](GetLoggers.html)           | Displays the names of all Splice Machine loggers in the system. |
| [SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL](SetLoggerLevel.html) | Changes the log level of the specified logger.                  |

[]()Statement and Stored Procedures System Procedures

These are the system procedures and functions for working with executing statements and stored procedures:

| Procedure / Function Name                                                            | Description                                                                                                                 |
|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_EMPTY\_GLOBAL\_STATEMENT\_CACHE](EmptyGlobalStatementCache.html) | Removes as many compiled statements (plans) as possible from the database-wide statement cache (across all region servers). |
| [SYSCS\_UTIL.SYSCS\_EMPTY\_STATEMENT\_CACHE](EmptyStatementCache.html)               | Removes as many compiled statements (plans) as possible from the database statement cache on your current region server.    |
| [SYSCS\_UTIL.SYSCS\_INVALIDATE\_STORED\_STATEMENTS](InvalidateStoredStatements.html) | Invalidates all system prepared statements and forces the query optimizer to create new execution plans.                    |
| [SYSCS\_UTIL.SYSCS\_UPDATE\_ALL\_SYSTEM\_PROCEDURES](UpdateAllSystemProcedures.html) | Updates the signatures of all of the system procedures in a database.                                                       |
| [SYSCS\_UTIL.SYSCS\_UPDATE\_SYSTEM\_PROCEDURE](UpdateSystemProcedure.html)           | Updates the stored declaration of a specific system procedure in the data dictionary.                                       |

[]()Statistics Procedures and Functions

These are the system procedures and functions for managing database statistics:

| Procedure / Function Name                                          | Description                                                        |
|--------------------------------------------------------------------|--------------------------------------------------------------------|
| [SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS](CollectSchemaStats.html) | Collects statistics on a specific schema in your database.         |
| [SYSCS\_UTIL.DISABLE\_COLUMN\_STATISTICS](DisableColumnStats.html) | Disables collection of statistics on a specific column in a table. |
| [SYSCS\_UTIL.DROP\_SCHEMA\_STATISTICS](DropSchemaStats.html)       | Drops statistics for a specific schema in your database.           |
| [SYSCS\_UTIL.ENABLE\_COLUMN\_STATISTICS](EnableColumnStats.html)   | Enables collection of statistics on a specific column in a table.  |

[]()System Status Procedures and Functions

These are the system procedures and functions for monitoring and adjusting system status:

| Procedure / Function Name                                                            | Description                                                                                |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_GET\_ACTIVE\_SERVERS](GetActiveServers.html)                     | Displays the number of active servers in the Splice cluster.                               |
| [SYSCS\_UTIL.SYSCS\_GET\_REGION\_SERVER\_STATS\_INFO](GetRegionServerStatsInfo.html) | Displays input and output statistics about the cluster.                                    |
| [SYSCS\_UTIL.SYSCS\_GET\_REQUESTS](GetRequests.html)                                 | Displays information about the number of RPC requests that are coming into Splice Machine. |
| [SYSCS\_UTIL.SYSCS\_GET\_VERSION\_INFO](GetVersionInfo.html)                         | Sets the connection access permission for the specified user.                              |
| [SYSCS\_UTIL.SYSCS\_GET\_WRITE\_INTAKE\_INFO](GetWriteIntakeInfo.html)               | Displays information about the number of writes coming into Splice Machine.                |

[]()Transaction Procedures and Functions

These are the system procedures and functions for working with transactions in your database

| Procedure / Function Name                                                  | Description                                                 |
|----------------------------------------------------------------------------|-------------------------------------------------------------|
| [SYSCS\_UTIL.SYSCS\_GET\_CURRENT\_TRANSACTION](GetCurrentTransaction.html) | Displays summary information about the current transaction. |

For access to the full source code for Splice Machine, visit [our open source GitHub repository](https://github.com/splicemachine/spliceengine "Click to navigate to the Splice Machine Open Source GitHub repository (opens in new tab)"): 

 


