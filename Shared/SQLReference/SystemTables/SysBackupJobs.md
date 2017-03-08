[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysBackupJobs.html)

SYSBACKUPJOBS System Table
==========================

The <span class="CodeFont">SYSBACKUPJOBS</span> table maintains information about all backup jobs that have been created for the database.

| Column Name      | Type      | Length | Nullable | Contents                                                                                                               |
|------------------|-----------|--------|----------|------------------------------------------------------------------------------------------------------------------------|
| JOB\_ID          | BIGINT    | 19     | NO       | The ID of this backup job.                                                                                             |
| FILESYSTEM       | VARCHAR   | 4000   | NO       | The backup destination directory.                                                                                      |
| TYPE             | VARCHAR   | 32     | NO       | The backup type; possible values are: <span class="CodeFont">incremental</span> or <span class="CodeFont">full</span>. |
| HOUR\_OF\_DAY    | INTEGER   | 10     | NO       | The regularly scheduled start time (in GMT hours) of the backup job if it is a daily backup.                           |
| BEGIN\_TIMESTAMP | TIMESTAMP | 29     | NO       | When this job was submitted.                                                                                           |

 


