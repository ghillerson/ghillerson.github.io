[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysBackupItems.html)

SYSBACKUPITEMS System Table
===========================

The <span class="CodeFont">SYSBACKUPITEMS</span> table maintains information about each item (table) backed up during a backup.

| Column Name      | Type      | Length | Nullable | Contents                                            |
|------------------|-----------|--------|----------|-----------------------------------------------------|
| BACKUP\_ID       | BIGINT    | 19     | NO       | The backup ID.                                      |
| ITEM             | VARCHAR   | 32642  | NO       | The name of the item.                               |
| BEGIN\_TIMESTAMP | TIMESTAMP | 29     | NO       | The start time of backing up this item.             |
| END\_TIMESTAMP   | TIMESTAMP | 29     | YES      | The end time of backing up this item.               |
| SNAPSHOT\_NAME   | VARCHAR   | 32642  | NO       | The name of the snapshot associated with this item. |

 


