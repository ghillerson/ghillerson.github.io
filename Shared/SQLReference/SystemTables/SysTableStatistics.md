[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysTableStatistics.html)

[]()SYSTABLESTATISTICS System Table
===================================

The <span class="CodeFont">SYSTABLESTATISTICS</span> table view describes the statistics for tables within the current database.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="CodeFont">SYS.SYSTABLESTATISTICS</span> is a system view.

The following table shows the contents of the <span class="CodeFont">SYSTABLESTATISTICS</span> system table.

| Column Name          | Type    | Length | Nullable | Contents                                                                                                                     |
|----------------------|---------|--------|----------|------------------------------------------------------------------------------------------------------------------------------|
| SCHEMANAME           | VARCHAR | 32672  | YES      | The name of the schema                                                                                                       |
| TABLENAME            | VARCHAR | 32672  | YES      | The name of the table                                                                                                        |
| CONGLOMERATENAME     | VARCHAR | 32672  | YES      | The name of the table                                                                                                        |
| TOTAL\_ROW\_COUNT    | BIGINT  | 19     | YES      | The total number of rows in the table                                                                                        |
| AVG\_ROW\_COUNT      | BIGINT  | 19     | YES      | The average number of rows in the table                                                                                      |
| TOTAL\_SIZE          | BIGINT  | 19     | YES      | The total size of the table                                                                                                  |
| NUM\_PARTITIONS      | BIGINT  | 19     | YES      | The number of partitions<span class="Footnote">1</span> for which statistics were collected.                                 |
| AVG\_PARTITION\_SIZE | BIGINT  | 19     | YES      | The average size of a single partition<span class="Footnote">1</span>, in bytes.                                             |
| ROW\_WIDTH           | BIGINT  | 19     | YES      | The <span class="ItalicFont">maximum average</span> of the widths of rows in the table, across all partitions, in bytes.     
                                                                                                                                                                                    
                                                      Each partition records the average width of a single row. This value is the maximum of those averages across all partitions.  |

> <span class="Footnote">1</span>Currently, a <span class="ItalicFont">partition</span> is equivalent to a region. In the future, we may use a more finely-grained definition for partition.

See Also

-   [About System Tables](Intro.SystemTables.html)
-   <span class="CodeFont">[SYSCOLUMNSTATISTICS](SysColumnStatistics.html)</span> system table

 


