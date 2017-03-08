[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/CollectSchemaStats.html)

SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS
=======================================

The <span class="CodeFont">SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS</span>  system procedure collects statistics on a specific schema in your database.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>Once statistics have been collected for a schema, they are automatically used by the query optimizer.

This procedure collects statistics for every table in the schema. It also collects statistics for the index associated with every table in the schema. For example, if you have :

-   a schema named <span class="CodeFont">mySchema</span>
-   <span class="CodeFont">mySchema</span> contains two tables: <span class="CodeFont">myTable1</span> and <span class="CodeFont">myTable2</span>
-   <span class="CodeFont">myTable1</span> has two indices: <span class="CodeFont">myTable1Index1</span> and <span class="CodeFont">myTable1Index2</span>

Then <span class="CodeFont">SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS</span> will collect statistics for <span class="CodeFont">myTable1</span>, <span class="CodeFont">myTable2</span>, <span class="CodeFont">myTable1Index1</span>, and <span class="CodeFont">myTable1Index2</span>.

Syntax

``` FcnSyntax
SYSCS_UTIL.COLLECT_SCHEMA_STATISTICS(
                     VARCHAR(128) schema,
                     BOOLEAN staleOnly
)
```

schemaName

Specifies the schema for which you want to collect statistics. Passing a <span class="CodeFont">null</span> or non-existent schema name generates an error.

staleOnly

A <span class="CodeFont">BOOLEAN</span> value that specifies:

-   If this is <span class="CodeFont">true</span>, data is only re-collected for partitions that are known to have out of date statistics.
-   If this is <span class="CodeFont">false</span>, data is collected on all partitions. <span class="Highlighted">Note</span> that this can significantly increase the time required to collect statistics, and is typically used only when you are not sure about the current quality of statistics in the entire schema.

The <span class="CodeItalicFont">staleOnly</span> parameter value is currently ignored, but must be specified in your call to this procedure. Its value is always set to <span class="CodeFont">false</span> in the system code.

Results

This procedure returns a results table that contains:

-   one row for each table
-   one row per index for every table and its associated index in the schema

Each row contains the following columns:

| Column Name   | Type    | Contents                                                   |
|---------------|---------|------------------------------------------------------------|
| schemaName    | VARCHAR | The name of the schema.                                    |
| tableName     | VARCHAR | The name of the table.                                     |
| partition     | VARCHAR | The name of the region on which statistics were collected. |
| rowsCollected | INTEGER | The number of rows of statistics that were collected..     |
| partitionSize | BIGINT  | The size of the partition in bytes.                        |

Usage Notes

Collecting statistics on a schema can take some time.

SQL Examples

``` Example
splice> CALL SYSCS_UTIL.COLLECT_SCHEMA_STATISTICS( 'SPLICE', false );
schemaName |tableName  |partition                               |rowsCollec&|partitionSize 
------------------------------------------------------------------------------------------
SPLICE     |PLAYERS    |splice:1440,,1467393447889.cbc33f4635ade|76         |3515           
SPLICE     |SALARIES   |splice:1456,,1467393749257.7724e0cb12af3|76         |1420           
SPLICE     |BATTING    |splice:1472,,1467393754889.b34f5da64c36e|44         |22571          
SPLICE     |PITCHING   |splice:1488,,1467393760434.35ee9880e5090|32         |21212          
SPLICE     |FIELDING   |splice:1504,,1467393775949.674b34acdb182|44         |9876           

5 rows selected
```

See Also

-   [Data Assignments and Comparisons](../DataTypes/DataTypeCompatability.html)
-   [<span class="CodeFont">SYSCS\_UTIL.ENABLE\_COLUMN\_STATISTICS</span>](EnableColumnStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.DISABLE\_COLUMN\_STATISTICS</span>](DisableColumnStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.DROP\_SCHEMA\_STATISTICS</span>](DropSchemaStats.html)
-   [Using Statistics](../../Developers/TuningAndDebugging/UsingStatistics.html) in the <span class="ItalicFont">Administrator's Guide</span>

 


