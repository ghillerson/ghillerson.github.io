[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysBackup.html)

SYSBACKUP System Table
======================

The <span class="CodeFont">SYSBACKUP</span> table maintains information about each database backup. You can query this table to find the ID of and details about a backup that was run at a specific time.

| Column Name                     | Type      | Length | Nullable | Contents                                                                                                                                          |
|---------------------------------|-----------|--------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| BACKUP\_ID                      | BIGINT    | 19     | NO       | The backup ID                                                                                                                                     |
| BEGIN\_TIMESTAMP                | TIMESTAMP | 29     | NO       | The start time of the backup                                                                                                                      |
| END\_TIMESTAMP                  | TIMESTAMP | 29     | YES      | The end time of the backup                                                                                                                        |
| STATUS                          | VARCHAR   | 10     | NO       | The status of the backup                                                                                                                          |
| FILESYSTEM                      | VARCHAR   | 32642  | NO       | The backup destination directory                                                                                                                  |
| SCOPE                           | VARCHAR   | 10     | NO       | The scope of the backup: database, schemas, tables, etc. The current allowable values are:                                                        
                                                                                                                                                                                                                      
                                                                   -   <span class="CodeFont">D</span> for the entire database                                                                                        |
| INCREMENTAL\_BACKUP             | BOOLEAN   | 1      | NO       | <span class="CodeFont">YES</span> for incremental backups, <span class="CodeFont">NO</span> for full backups                                      
                                                                                                                                                                                                                      
                                                                   <span class="BoldFont">NOTE:</span> Incremental backups are not yet available.                                                                     |
| INCREMENTAL\_PARENT\_BACKUP\_ID | BIGINT    | 19     | YES      | For an incremental backup, this is the <span class="CodeFont">BACKUP\_ID</span> of the previous backup on which this incremental backup is based. 
                                                                                                                                                                                                                      
                                                                   For full backups, this is <span class="CodeFont">-1</span>.                                                                                        
                                                                                                                                                                                                                      
                                                                   <span class="BoldFont">NOTE:</span> Incremental backups are not yet available.                                                                     |
| BACKUP\_ITEM                    | INTEGER   | 10     | YES      | The number of tables that were backed up.                                                                                                         |

 


