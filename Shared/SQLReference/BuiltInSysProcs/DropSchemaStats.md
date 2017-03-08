[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/DropSchemaStats.html)

SYSCS\_UTIL.DROP\_SCHEMA\_STATISTICS
====================================

The <span class="CodeFont">SYSCS\_UTIL.DROP\_SCHEMA\_STATISTICS</span>  system procedure drops statistics for a specific schema in your database.

This procedure drops statistics for every table in the schema. It also drops statistics for the index associated with every table in the schema. For example, if you have :

-   a schema named <span class="CodeFont">mySchema</span>
-   <span class="CodeFont">mySchema</span> contains two tables: <span class="CodeFont">myTable1</span> and <span class="CodeFont">myTable2</span>
-   <span class="CodeFont">myTable1</span> has two indices: <span class="CodeFont">myTable1Index1</span> and <span class="CodeFont">myTable1Index2</span>

Then <span class="CodeFont">SYSCS\_UTIL.DROP\_SCHEMA\_STATISTICS</span> will drop statistics for <span class="CodeFont">myTable1</span>, <span class="CodeFont">myTable2</span>, <span class="CodeFont">myTable1Index1</span>, and <span class="CodeFont">myTable1Index2</span>.

Syntax

``` FcnSyntax
SYSCS_UTIL.DROP_SCHEMA_STATISTICS( VARCHAR(128) schema );
```

schemaName

Specifies the schema for which you want to drop statistics. Passing a <span class="CodeFont">null</span> or non-existent schema name generates an error.

Results

This procedure does not produce a result.

SQL Examples

``` Example
splice> CALL SYSCS_UTIL.DROP_SCHEMA_STATISTICS('MYSCHEMA');
Statement executed.
```

See Also

-   [Data Assignments and Comparisons](../DataTypes/DataTypeCompatability.html)
-   [<span class="CodeFont">SYSCS\_UTIL.ENABLE\_COLUMN\_STATISTICS</span>](EnableColumnStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.DISABLE\_COLUMN\_STATISTICS</span>](DisableColumnStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS</span>](CollectSchemaStats.html)
-   [Using Statistics](../../Developers/TuningAndDebugging/UsingStatistics.html) in the <span class="ItalicFont">Administrator's Guide</span>

 


