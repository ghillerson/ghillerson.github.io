[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysFiles.html)

<a href="" id="SystemTables.SysFiles"></a>[]()SYSFILES System Table
===================================================================

The <span class="CodeFont">SYSFILES</span> table describes jar files stored in the database.

The following table shows the contents of the <span class="CodeFont">SYSFILES</span> system table.

| Column Name  | Type    | Length | Nullable | Contents                                                                                               |
|--------------|---------|--------|----------|--------------------------------------------------------------------------------------------------------|
| FILEID       | CHAR    | 36     | NO       | Unique identifier for the jar file                                                                     |
| SCHEMAID     | CHAR    | 36     | NO       | ID of the jar file's schema (join with <span class="CodeFont">SYSSCHEMAS.SCHEMAID</span>)              |
| FILENAME     | VARCHAR | 128    | NO       | SQL name of the jar file                                                                               |
| GENERATIONID | BIGINT  | 19     | NO       | Generation number for the file. When jar files are replaced, their generation identifiers are changed. |

See Also

-   [About System Tables](Intro.SystemTables.html)

 


