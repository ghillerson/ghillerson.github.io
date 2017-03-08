[Open topic with navigation](../../../index.html#Shared/SQLReference/SystemTables/SysColumnStatistics.html)

[]()SYSCOLUMNSTATISTICS System Table
====================================

The <span class="CodeFont">SYSCOLUMNSTATISTICS</span> table view describes the statistics for a specific table column within the current database.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span><span class="CodeFont">SYS.SYSCOLUMNSTATISTICS</span> is a system view.

The following table shows the contents of the <span class="CodeFont">SYSCOLUMNSTATISTICS</span> system table.

| Column Name    | Type    | Length | Nullable | Contents                                                                |
|----------------|---------|--------|----------|-------------------------------------------------------------------------|
| SCHEMANAME     | VARCHAR | 32672  | YES      | The name of the schema.                                                 |
| TABLENAME      | VARCHAR | 32672  | YES      | The name of the table.                                                  |
| COLUMNNAME     | VARCHAR | 32672  | YES      | The name of the column.                                                 |
| CARDINALITY    | BIGINT  | 19     | YES      | The estimated number of distinct values for the column.                 |
| NULL\_COUNT    | BIGINT  | 19     | YES      | The number of rows in the table that have NULL for the column.          |
| NULL\_FRACTION | REAL    | 23     | YES      | The ratio of <span class="CodeFont">NULL</span> records to all records: 
                                                                                                                         
                                                ``` PlainCell                                                            
                                                NULL_COUNT / TOTAL_ROW_COUNT                                             
                                                ```                                                                      |
| MIN\_VALUE     | VARCHAR | 32672  | YES      | The minimum value for the column.                                       |
| MAX\_VALUE     | VARCHAR | 32672  | YES      | The maximum value for the column.                                       |
| QUANTILES      | VARCHAR | 32672  | YES      | The quantiles statistics sketch for the column.                         |
| FREQUENCIES    | VARCHAR | 32672  | YES      | The frequencies statistics sketch for the column.                       |
| THETA          | VARCHAR | 32672  | YES      | The theta statistics sketch for the column.                             |

The <span class="CodeFont">QUANTILES</span>, <span class="CodeFont">FREQUENCIES</span>, and <span class="CodeFont">THETA</span> values are all sketches computed using the Yahoo Data Sketches library, which you can read about here: <https://datasketches.github.io/>

See Also

-   [About System Tables](Intro.SystemTables.html)
-   <span class="CodeFont">[SYSTABLESTATISTICS](SysTableStatistics.html)</span> system table

 


