[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/DisableColumnStats.html)

SYSCS\_UTIL.DISABLE\_COLUMN\_STATISTICS
=======================================

The <span class="CodeFont">SYSCS\_UTIL.DISABLE\_COLUMN\_STATISTICS</span>  system procedure disables collection of statistics on a specific table column in your database.

Syntax

``` FcnSyntax
SYSCS_UTIL.DISABLE_COLUMN_STATISTICS(
                       VARCHAR(128) schema,
                       VARCHAR(128) table,
                       VARCHAR(128) columnName)
```

schemaName

Specifies the schema of the table. Passing a <span class="CodeFont">null</span> or non-existent schema name generates an error.

tableName

Specifies the table name of the table. The string must exactly match the case of the table name, and the argument of <span class="CodeFont">"Fred"</span> will be passed to SQL as the delimited identifier <span class="CodeFont">'Fred'</span>. Passing a <span class="CodeFont">null</span> or non-existent table name generates an error.

columnName

Specifies the name of the column for which you want statistics disabled. Passing a <span class="CodeFont">null</span> or non-existent column name generates an error.

Results

This procedure does not return a result.

Usage Notes

Statistics are automatically collected on all columns by default. Attempting to disable statistics collection on a keyed column generates an error.

SQL Examples

``` Example
splice> CALL SYSCS_UTIL.DISABLE_COLUMN_STATISTICS('SPLICE', 'Salaries', 'Salary');
Statement executed.
```

See Also

-   [Data Assignments and Comparisons](../DataTypes/DataTypeCompatability.html)
-   [<span class="CodeFont">SYSCS\_UTIL.ENABLE\_COLUMN\_STATISTICS</span>](EnableColumnStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.COLLECT\_SCHEMA\_STATISTICS</span>](CollectSchemaStats.html)
-   [<span class="CodeFont">SYSCS\_UTIL.DROP\_SCHEMA\_STATISTICS</span>](DropSchemaStats.html)
-   [Using Statistics](../../Developers/TuningAndDebugging/UsingStatistics.html) in the <span class="ItalicFont">Administrator's Guide</span>

 


